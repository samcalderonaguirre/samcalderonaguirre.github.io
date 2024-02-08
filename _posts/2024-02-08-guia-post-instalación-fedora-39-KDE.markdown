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

