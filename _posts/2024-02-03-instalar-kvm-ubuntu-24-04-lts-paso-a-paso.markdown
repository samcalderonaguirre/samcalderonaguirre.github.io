---
layout: post
title:  Cómo instalar KVM en Ubuntu 24.04 LTS paso a paso (Spanish)
date:   2024-02-03 17:23:23 +0300
image:  13.jpg
tags:   Linux
---

<p align="justify">KVM, abreviatura de Kernel-Based Virtual Machine, es una tecnología de virtualización de código abierto integrada en el kernel de Linux. Un hipervisor de tipo 1 (bare metal) que permite que el kernel actúe como un hipervisor bare metal. </p>

<p align="justify">KVM permite a los usuarios crear y ejecutar múltiples computadoras invitadas, como Windows y Linux. Cada máquina invitada funciona independientemente de otras máquinas virtuales y del sistema operativo subyacente (sistema host) y tiene sus propios recursos informáticos, incluidos CPU, RAM, interfaces de red y almacenamiento.</p>

###### Requisitos previos

{% highlight markdown %}
* Ubuntu 24.04 LTS preinstalado
* 2 vCPU y 4 GB de RAM
* Conectividad a Internet estable
{% endhighlight %}

###### 1) Actualizar Ubuntu 24.04 LTS

<p align="justify">Para comenzar, inicie la terminal y realice una actualización de la paquetería local del sistema de la siguiente manera.</p>

{% highlight shell %}
  $ sudo apt update
{% endhighlight %}

![]({{site.baseurl}}/images/14.png)

###### 2) Compruebe si la virtualización está habilitada

<p align="justify">Antes de continuar, debe verificar si su CPU admite la virtualización KVM. Para que esto sea posible, su sistema debe tener un procesador Intel VT-x (vmx) o un procesador AMD-V (svm).</p>

<p align="justify">Esto se logra ejecutando el siguiente comando. si la salida es mayor que 0, entonces la virtualización está habilitada. De lo contrario, la virtualización estará deshabilitada y deberá habilitarla.</p>

{% highlight shell %}
  $ egrep -c '(vmx|svm)' /proc/cpuinfo
{% endhighlight %}

![]({{site.baseurl}}/images/15.png)

<p align="justify">Del resultado anterior, puede deducir que la virtualización está habilitada ya que el resultado impreso es mayor que 0. Si la virtualización no está habilitada, asegúrese de habilitar la función de virtualización en la configuración del BIOS de su sistema.</p>

<p align="justify">Además, puede verificar si la virtualización KVM está habilitada ejecutando el siguiente comando:</p>

{% highlight shell %}
  $ kvm-ok
{% endhighlight %}

<p align="justify">Para que esto funcione, debe haber instalado el paquete cpu-checker; de lo contrario, se encontrará con el error "Comando 'kvm-ok' no encontrado".</p>

<p align="justify">Directamente a continuación, recibirá instrucciones sobre cómo resolver este problema, es decir, instalar el paquete cpu-checker.</p>

{% highlight shell %}
  $ sudo apt install -y cpu-checker
{% endhighlight %}

![]({{site.baseurl}}/images/16.png)

###### 3) Instale KVM en Ubuntu 24.04

<p align="justify">A continuación, ejecute el siguiente comando para instalar KVM y paquetes de virtualización adicionales en Ubuntu.</p>

{% highlight shell %}
  $ sudo apt install -y qemu-kvm virt-manager libvirt-daemon-system virtinst libvirt-clients bridge-utils
{% endhighlight %}

<p align="justify">Analicemos los paquetes que estamos instalando:</p>

{% highlight markdown %}
* qemu-kvm: un emulador de código abierto y un paquete de virtualización que proporciona emulación de hardware.
* virt-manager: una interfaz gráfica basada en Qt para administrar máquinas virtuales a través del servicio libvirt.
* libvirt-daemon-system: un paquete que proporciona los archivos de configuración necesarios para ejecutar el servicio libvirt.
* virtinst: un conjunto de utilidades de línea de comandos para aprovisionar y modificar máquinas virtuales.
* libvirt-clients: un conjunto de bibliotecas y API del lado del cliente para administrar y controlar máquinas virtuales e hipervisores desde la línea de comandos.
* bridge-utils: un conjunto de herramientas para crear y administrar dispositivos puente.
{% endhighlight %}

###### 4) Iniciar y habilitar el servicio de virtualización

<p align="justify">Con todos los paquetes instalados, habilite e inicie el servicio Libvirt.</p>

{% highlight shell %}
  $ sudo systemctl enable --now libvirtd
  $ sudo systemctl start libvirtd
{% endhighlight %}

<p align="justify">Confirme que el servicio de virtualización se esté ejecutando como se muestra.</p>

{% highlight shell %}
  $ sudo systemctl status libvirtd
{% endhighlight %}

![]({{site.baseurl}}/images/17.png)