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

