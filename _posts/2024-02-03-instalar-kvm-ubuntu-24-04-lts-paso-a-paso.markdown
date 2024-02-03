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