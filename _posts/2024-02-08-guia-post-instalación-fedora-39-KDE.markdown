---
layout: post
title:  Guía de configuración de Fedora 39 con KDE Plasma después de la instalación (Spanish)
date:   2024-02-08 17:23:23 +0300
image:  22.jpg
tags:   Linux
---

<p align="justify">Fedora es una distribución muy limpia cuando se trata de software gratuito, que contiene esencialmente solo controladores y firmware que pertenecen a la rama oficial de Linux para mejorar el soporte de hardware. De lo contrario, los usuarios encontrarán pocos componentes propietarios en el almacenamiento del sistema, lo que los limitará en aspectos como la reproducción de contenidos multimedia y las capacidades de interacción. </p>

#### Instalación de los Repositorios Free y Nonfree

* <p align="justify"><b>Free</b> s para software de código abierto (según lo definido por las Pautas de licencia de Fedora) que el proyecto Fedora no puede distribuir debido a otras razones.</p>
* <p align="justify"><b>Nonfree</b> para para software redistribuible que no sea software de código abierto (según lo definido por las Pautas de licencia de Fedora); esto incluye software con código fuente disponible públicamente que no tiene restricciones de tipo "no comercial."</p>

<p align="justify">La instalación se puede realizar mediante un navegador web o mediante la línea de comando. En esta guía usaremos la línea de comandos.</p>

<p align="justify">Primero haga una actualización de sus sistema con el siguiente comando:</p>

{% highlight shell %}
  $ sudo dnf update -y
{% endhighlight %}

<p align="justify">Instalar los respositorios free y nonfree:</p>

{% highlight shell %}
  $ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
{% endhighlight %}

![]({{site.baseurl}}/images/23.png)

<p align="justify">En Fedora, se utiliza de forma predeterminada la biblioteca openh264, por lo que necesita que el repositorio esté habilitado explícitamente:</p>

{% highlight shell %}
  $ sudo dnf config-manager --enable fedora-cisco-openh264
{% endhighlight %}

<p align="justify">Tendrás que reiniciar para que aparezcan los repositorios de rpmfusion.</p>


#### Metadatos de AppStream

<p align="justify">Los repositorios de RPM Fusion también proporcionan metadatos de Appstream para permitir a los usuarios instalar paquetes utilizando Gnome Software/KDE Discover. Tenga en cuenta que estos son un subconjunto de todos los paquetes, ya que los metadatos solo se generan para paquetes GUI.</p>

<p align="justify">Para las versiones actuales de Fedora: el método sugerido es instalar appstream-data usando DNF.</p>

<p align="justify">El siguiente comando instalará los paquetes necesarios:</p>

{% highlight shell %}
  $ sudo dnf groupupdate core
{% endhighlight %}

![]({{site.baseurl}}/images/24.png)

<p align="justify">Presione la tecla S para terminar la instalación de los paquetes rpmfusion-free-appstream-data rpmfusion-nonfree-appstream-data.</p>


#### Configurar Flathub

<p align="justify">Flatpak se instala de forma predeterminada en Fedora Workstation, Fedora Silverblue y Fedora Kinoite. Para comenzar, todo lo que necesitas hacer es habilitar Flathub, que es la mejor manera de obtener aplicaciones Flatpak. Simplemente descargue e instale el <a href="https://dl.flathub.org/repo/flathub.flatpakrepo">el archivo del repositorio Flathub</a>.</p>

<p align="justify">Los enlaces anteriores deberían funcionar en las instalaciones predeterminadas de GNOME y KDE Fedora, pero si fallan por algún motivo, puede agregar manualmente el control remoto Flathub ejecutando:</p>

{% highlight shell %}
  $ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
{% endhighlight %}


#### Activar otros repositorios para Fedora 39 desde la tienda Discover de KDE Plasma

<p align="justify">Haga clic en la tienda Discover, después en Preferencias, y marque las opciones de repositorios que ofrece Fedora, por ejemplo los repositorios de Google y del driver propietario de NVIDIA.</p>

![]({{site.baseurl}}/images/25.png)

<p align="justify">Ejecute el siguiente comando en la terminal para actualizar los repositorios.</p>

{% highlight shell %}
  $ sudo dnf update
{% endhighlight %}

![]({{site.baseurl}}/images/26.png)


#### Multimedia en Fedora

###### Cambiar a ffmpeg completo

<p align="justify">Fedora ffmpeg-free funciona la mayor parte del tiempo, pero de vez en cuando se experimentarán versiones que no coinciden. Cambie a la compilación ffmpeg proporcionada por rpmfusion que sea mejor compatible. Aún deberá seguir la siguiente sección para obtener códecs o complementos adicionales relacionados con los paquetes que pueda haber instalado.</p>


{% highlight shell %}
  $ sudo dnf swap ffmpeg-free ffmpeg --allowerasing
{% endhighlight %}


###### Instalar códecs adicionales

<p align="justify">Esto permitirá que la aplicación que utiliza el marco gstreamer y otro software multimedia reproduzca otros códecs restringidos. El siguiente comando instalará los paquetes multimedia complementarios que necesitan las aplicaciones habilitadas para gstreamer:</p>

{% highlight shell %}
  $ sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
{% endhighlight %}

<p align="justify">El siguiente comando instalará los paquetes complementarios de sonido y vídeo que necesitan algunas aplicaciones:</p>

{% highlight shell %}
  $ sudo dnf groupupdate sound-and-video
{% endhighlight %}

###### Instalar otros codecs y compresores.

<p align="justify">Tras configurar los repositorios de RPM Fusion, en primer lugar vamos a instalar los paquetes básicos para la multimedia, el soporte de RAW y WebP para el visor de imágenes, la aplicación File-Roller (que ahora no viene preinstalada), el compresor/descompresor 7Zip y el descompresor UNRAR: </p>

{% highlight shell %}
  $ sudo dnf install gstreamer1-libav gstreamer1-plugins-bad-free-extras gstreamer1-plugins-bad-freeworld gstreamer1-plugins-good-extras gstreamer1-plugins-ugly unrar p7zip p7zip-plugins gstreamer1-plugin-openh264 mozilla-openh264 openh264 webp-pixbuf-loader gstreamer1-plugins-bad-free-fluidsynth gstreamer1-plugins-bad-free-wildmidi gstreamer1-svt-av1 libopenraw-pixbuf-loader dav1d file-roller
{% endhighlight %}


###### Instalar el soporte para VA-API (aceleración por hardware) de Gstreamer

{% highlight shell %}
  $ sudo dnf install gstreamer1-vaapi libva libva-utils
{% endhighlight %}


###### Aceleración por hardware

<p align="justify">Para aquellos que usen una gráfica de Intel (por ahora solo las integradas incluidas en sus propios procesadores) pueden obtener el soporte de aceleración por hardware instalando los siguientes paquetes: </p>

<p align="justify">Intel (reciente)</p>

{% highlight shell %}
  $ sudo dnf install intel-media-driver
{% endhighlight %}

<p align="justify">Intel (más viejo)</p>

{% highlight shell %}
  $ sudo dnf install libva-intel-driver
{% endhighlight %}


<p align="justify">Códecs de hardware con AMD (mesa)</p>

{% highlight shell %}
  $ sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
{% endhighlight %}

{% highlight shell %}
  $ sudo dnf swap mesa-vdpau-drivers mesa-vdpau-drivers-freeworld
{% endhighlight %}

<p align="justify">Si utiliza bibliotecas compatibles con i686 (para Steam o similares):</p>

{% highlight shell %}
  $ sudo dnf swap mesa-va-drivers.i686 mesa-va-drivers-freeworld.i686
{% endhighlight %}

{% highlight shell %}
  $ sudo dnf swap mesa-vdpau-drivers.i686 mesa-vdpau-drivers-freeworld.i686
{% endhighlight %}


<p align="justify">Códecs de hardware con NVIDIA, el controlador propietario de Nvidia no es compatible con VAAPI, pero existe un contenedor que puede unir NVDEC/NVENC con VAAPI.</p>

{% highlight shell %}
  $ sudo dnf install nvidia-vaapi-driver
{% endhighlight %}

<p align="justify">Reproducir un DVD</p>

{% highlight shell %}
  $ sudo dnf install rpmfusion-free-release-tainted
{% endhighlight %}

{% highlight shell %}
  $ sudo dnf install libdvdcss
{% endhighlight %}


###### Renderización de vídeo

<p align="justify">En la actualidad hay muchos editores de vídeo Open Source de calidad que se adaptan bien a esos usuarios sin profundos conocimientos del tema, como Avidemux, Shotcut y Kdenlive. Para renderizar vídeos con populares formatos como x264 y x265 solo hay que instalar lo siguiente: </p>

{% highlight shell %}
  $ sudo dnf install x264 h264enc x265 svt-av1 rav1e
{% endhighlight %}




#### Instalación del controlador NVIDIA

<p align="justify">NVIDIA tiene varias series de controladores, cada una de las cuales tiene un soporte de hardware diferente. Para determinar qué controlador necesita instalar, primero deberá encontrar el modelo de su tarjeta gráfica.</p>

<p align="justify">Si no lo sabes escriba el siguiente comando en la terminal:</p>

{% highlight shell %}
  $ /sbin/lspci | grep -e VGA
{% endhighlight %}

<p align="justify">Probablemente estés en el caso Optimus si tu tarjeta NVIDIA se encuentra con el siguiente comando:</p>

{% highlight shell %}
  $ /sbin/lspci | grep -e 3D
{% endhighlight %}

<p align="justify">Instale los siguientes paquetes como requisitos para la instalación del controlador: </p>

{% highlight shell %}
  $ sudo dnf update -y
{% endhighlight %}

{% highlight shell %}
  $ sudo dnf install gcc kernel-headers kernel-devel
{% endhighlight %}

<p align="justify">Instale el contralador de NVIDIA:  </p>

{% highlight shell %}
  $ sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda -y
{% endhighlight %}

<p align="justify">Instalación de CUDA: </p>

{% highlight shell %}
  $ sudo dnf install xorg-x11-drv-nvidia-cuda -y
{% endhighlight %}

<p align="justify">Suspensión</p>

{% highlight shell %}
  $ sudo dnf install xorg-x11-drv-nvidia-power -y
{% endhighlight %}

{% highlight shell %}
  $ sudo systemctl enable nvidia-{suspend,resume,hibernate}
{% endhighlight %}

<p align="justify">Instalación de VULKAN</p>

{% highlight shell %}
  $ sudo dnf install vulkan -y
{% endhighlight %}

{% highlight shell %}
  $ sudo systemctl enable nvidia-{suspend,resume,hibernate}
{% endhighlight %}

<p align="justify">Instalación de NVENC/NVDEC</p>

{% highlight shell %}
  $ sudo dnf install xorg-x11-drv-nvidia-cuda-libs -y
{% endhighlight %}

<p align="justify">Otros paquetes de NVIDIA</p>

{% highlight shell %}
  $ sudo dnf install xorg-x11-drv-nvidia xorg-x11-drv-nvidia-libs xorg-x11-drv-nvidia-libs.i686 -y
{% endhighlight %}


#### Configuración gráfica básica de SELinux y el cortafuegos

{% highlight shell %}
  $ sudo dnf install policycoreutils-gui firewall-config -y
{% endhighlight %}