---
layout: post
title:  Darktable Flatpak no muestra imágenes en Fedora 43 (Wayland + NVIDIA) – Solución 💻🛠️
date:   2025-12-21 22:23:23 +0300
image:  darktable-01.jpg
tags:   Linux
---

## Contexto

Al utilizar **Darktable en formato Flatpak** sobre **Fedora 43**, con **GNOME 49 en sesión Wayland** y una **GPU NVIDIA propietaria**, puede ocurrir que la aplicación inicie correctamente pero muestre una interfaz gris o vacía, sin cargar imágenes ni colecciones.

Este comportamiento **no es un fallo de Darktable**, sino un problema de compatibilidad entre:

- Wayland  
- Drivers propietarios NVIDIA  
- OpenCL dentro del sandbox de Flatpak  

El fallo se produce de forma silenciosa, sin mensajes de error visibles en la interfaz gráfica.

![Error de Darktable en Fedora 43]({{site.baseurl}}/images/Captura desde 2025-12-21 22-02-04.png)

---

## Síntomas

- Darktable inicia sin errores aparentes  
- La interfaz se muestra, pero:
  - No aparecen imágenes  
  - La colección está vacía  
  - El área central permanece gris  
- El problema ocurre principalmente en:
  - Sesión Wayland  
  - Versión Flatpak  
  - Sistemas con GPU NVIDIA  

---

## Causa técnica

Darktable intenta inicializar **OpenCL** para acelerar el procesamiento utilizando la GPU.  
En entornos **Wayland + NVIDIA + Flatpak**, esta inicialización puede fallar debido a:

- Limitaciones del sandbox de Flatpak  
- Problemas de integración entre EGL/OpenGL y Wayland  
- Runtimes NVIDIA que no coinciden exactamente con el driver instalado en el sistema  

Cuando OpenCL falla, Darktable no siempre hace un fallback correcto, lo que provoca una interfaz inutilizable aunque la aplicación esté “abierta”.

---

## Solución recomendada (probada)

La solución más simple y efectiva es **desactivar OpenCL para Darktable Flatpak**, forzando el uso de CPU.

Ejecuta el siguiente comando:

```bash
flatpak override --user --env=DT_OPENCL=0 org.darktable.Darktable
```

Luego, inicia Darktable normalmente.

## Resultado

- Darktable inicia correctamente

- La interfaz se renderiza sin problemas

- Las imágenes y colecciones se muestran con normalidad

- El sistema es estable bajo Wayland

## 📌 Impacto en rendimiento

La desactivación de OpenCL tiene un impacto mínimo en flujos de trabajo fotográficos habituales. Solo se nota en exportaciones masivas o procesos muy intensivos.