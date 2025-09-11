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


* <p align="justify"><b>qemu-kvm:</b> un emulador de código abierto y un paquete de virtualización que proporciona emulación de hardware.</p>
* <p align="justify"><b>virt-manager:</b> una interfaz gráfica basada en Qt para administrar máquinas virtuales a través del servicio libvirt.</p>
* <p align="justify"><b>libvirt-daemon-system:</b> un paquete que proporciona los archivos de configuración necesarios para ejecutar el servicio libvirt.</p>
* <p align="justify"><b>virtinst:</b> un conjunto de utilidades de línea de comandos para aprovisionar y modificar máquinas virtuales.</p>
* <p align="justify"><b>libvirt-clients:</b> un conjunto de bibliotecas y API del lado del cliente para administrar y controlar máquinas virtuales e hipervisores desde la línea de comandos.</p>
* <p align="justify"><b>bridge-utils:</b> un conjunto de herramientas para crear y administrar dispositivos puente.</p>



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

<p align="justify">Además, debe agregar el usuario actualmente conectado a los grupos kvm y libvirt para que puedan crear y administrar máquinas virtuales.</p>

{% highlight shell %}
  $ sudo usermod -aG kvm $USER
  $ sudo usermod -aG libvirt $USER
{% endhighlight %}

<p align="justify">La variable de entorno $USER apunta al nombre del usuario actualmente conectado. Para aplicar este cambio, debe cerrar sesión y volver a iniciarla.</p>
 


###### 5) Crear puente de red (br0) – Opcional

<p align="justify">Si planea acceder a máquinas virtuales KVM fuera de su sistema Ubuntu 24.04, debe asignar la interfaz de VM a un puente de red. A través de un puente virtual llamado virbr0, se crea automáticamente cuando se instala KVM pero se utiliza con fines de prueba.</p>

<p align="justify">Para crear un puente de red, cree el archivo '01-netcfg.yaml' con el siguiente contenido en la carpeta /etc/netplan.</p>

{% highlight shell %}
  $ sudo vi /etc/netplan/01-netcfg.yaml
  
  network:
  ethernets:
    enp0s3:
      dhcp4: false
      dhcp6: false
  # add configuration for bridge interface
  bridges:
    br0:
      interfaces: [enp0s3]
      dhcp4: false
      addresses: [192.168.1.162/24]
      macaddress: 08:00:27:4b:1d:45
      routes:
        - to: default
          via: 192.168.1.1
          metric: 100
      nameservers:
        addresses: [4.2.2.2]
      parameters:
        stp: false
      dhcp6: false
  version: 2
{% endhighlight %}

<p align="justify">Guardar y salir del archivo.</p>

<p align="justify"><b>Nota:</b> Estos detalles según mi configuración, así que reemplace las entradas de la dirección IP, el nombre de la interfaz y la dirección mac según su configuración.</p>

<p align="justify">Para aplicar el cambio anterior, ejecute ‘netplan apply’.</p>

{% highlight shell %}
  $ sudo netplan apply
{% endhighlight %}

<p align="justify">Verifique el puente de red 'br0', ejecute el siguiente comando ip.</p>

{% highlight shell %}
  $ ip add show
{% endhighlight %}

![]({{site.baseurl}}/images/18.png)

###### 6) Inicie el Administrador de máquinas virtuales KVM

<p align="justify">Con KVM instalado, puede comenzar a crear sus máquinas virtuales utilizando la herramienta GUI virt-manager. Para comenzar, utilice la utilidad de búsqueda de GNOME y busque "Administrador de máquinas virtuales".</p>

![]({{site.baseurl}}/images/19.png)

<p align="justify">Haga clic en el icono que aparece. Esto inicia la interfaz del administrador de máquinas virtuales.</p>

![]({{site.baseurl}}/images/20.png)

<p align="justify">De aquí podrá instalar los sistemas operativos de acuerdo a su trabajo.</p>

![]({{site.baseurl}}/images/21.png)