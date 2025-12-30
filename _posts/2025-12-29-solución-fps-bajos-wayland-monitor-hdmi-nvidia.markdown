---
layout: post
title:  ✅ Por qué bajan los FPS a la mitad al conectar un monitor HDMI en Wayland usando gráficos NVIDIA
date:   2025-12-29 22:23:23 +0300
image:  wayland-nvidia.jpg
tags:   Linux
---

En portátiles con NVIDIA + Intel (Optimus), en Wayland ocurre a menudo:

- Cuando conectas un monitor externo al HDMI, este está físicamente cableado a la GPU NVIDIA, no a la Intel.

- La pantalla interna usa Intel, pero el monitor externo usa NVIDIA → Wayland fuerza una especie de “frame copy” entre GPUs.

- Ese “frame copy” hace que el rendimiento caiga 40–60%.

Esto no pasa en X11 porque usa un modelo de composición diferente.

---

## ✅ Soluciones posibles (de mayor recomendación a menor)

### 1. Forzar la sesión a usar NVIDIA PRIME Render Offload correctamente

Primero revisa si estás en el driver propietario NVIDIA y no en nouveau:

```bash
nvidia-smi
```

Si te responde con info, perfecto.

Ahora activa Dynamic Boost + Dynamic Power Management:

Edita el archivo:

```bash
sudo nano /etc/modprobe.d/nvidia.conf
```

Agrega:

```bash
options nvidia NVreg_RegistryDwords="PowermizerEnable=0x1;PerfLevelSrc=0x2222"
options nvidia-drm modeset=1
```

Luego:

```bash
sudo dracut --force
sudo reboot
```

Esto mejora mucho los FPS en monitores externos.

---

### 2. Usar la sesión “Nvidia (Wayland)” (si aparece en Fedora 43)

En Fedora 43, GNOME soporta una sesión Wayland optimizada solo para NVIDIA, que evita el doble render.

Haz logout → en el selector de sesión elige:

GNOME on Wayland (NVIDIA)
o
GNOME on NVIDIA

Si existe, úsala.
Muchos usuarios reportan que así el problema desaparece.

---

### 3. Desactivar el “Hybrid Mode” de NVIDIA y activar modo “Full NVIDIA”

Esto elimina la mezcla Intel/Nvidia (evita el doble render).

Instala herramientas:

```bash
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```

Luego:

```bash
sudo dnf install switcheroo-control
sudo systemctl enable --now switcheroo-control
```

Ver GPU activa:

```bash
switcherooctl
```

Forzar todo el escritorio a usar NVIDIA:

```bash
sudo nano /etc/environment
```

Agrega:

```bash
__GLX_VENDOR_LIBRARY_NAME=nvidia
NV_PRIME_RENDER_OFFLOAD=1
COGL_RENDERER=nvidia
WLR_NO_HARDWARE_CURSORS=1
```

Reinicia.

Esto usa NVIDIA para ambas pantallas → FPS igual en interno y externo.
Mayor consumo energético, pero máximo rendimiento.

---

### 4. Intentar con X11 si Wayland sigue bajando FPS

Aunque Wayland es más moderno, NVIDIA todavía rinde mejor en X11 cuando hay monitores externos.

Logout → selecciona:

<b>GNOME on Xorg</b>

Si en Xorg tus FPS vuelven a lo normal → confirmas que es un problema de composición Wayland/NVIDIA.

---

### 5. Cambiar el puerto HDMI por DisplayPort si tu laptop tiene uno

Muchos equipos tienen Mini DisplayPort cableado directamente a la NVIDIA sin pasar por Intel → rendimiento perfecto.

Si tu modelo lo tiene, úsalo en vez de HDMI.

---

