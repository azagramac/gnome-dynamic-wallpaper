## 🖼️ Fondos dinámicos en GNOME

GNOME permite definir fondos de pantalla que cambian automáticamente entre una
imagen clara y otra oscura usando un descriptor XML.

Modo claro → day.*
Modo oscuro → night.*

Se han incluido los fondos de pantalla de Fedora 33, 37 y 43. 
Se pueden decargar mas desde la [wiki de fedora](https://fedoraproject.org/wiki/Wallpapers)


## 📁 Estructura del repositorio

```text
.
├── fedora33/
│   ├── day.jpg
│   └── night.jpg
├── fedora37/
│   ├── day.jpg
│   └── night.jpg
├── fedora43/
│   ├── day.png
│   └── night.png
├── fedora-dynamic.xml
└── README.md
```

## 📦 Instalación
1. Clonar repositorio
```bash
git clone https://github.com/azagramac/gnome-dynamic-wallpaper.git
cd gnome-dynamic-wallpaper
```

2. Copiar fondos
```bash
mkdir -p ~/.local/share/backgrounds
cp -r fedora33 fedora37 fedora43 ~/.local/share/backgrounds/
```

3. Copiar el descriptor XML
```bash
mkdir -p ~/.local/share/gnome-background-properties
cp fedora-dynamic.xml ~/.local/share/gnome-background-properties/
```
> ⚠️  GNOME requiere rutas absolutas (file:///home/usuario/...)
	El XML incluido asume que los fondos están en ~/.local/share/backgrounds/.


## 🌗 Cambiar el modo claro / oscuro manualmente
Modo claro
```bash
gsettings set org.gnome.desktop.interface color-scheme 'default'
```

Modo oscuro
```bash
gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'
```

## ⏱️ Cambio automático

```bash
0 8 * * * DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus gsettings set org.gnome.desktop.interface color-scheme 'default'
0 19 * * * DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus gsettings set org.gnome.desktop.interface color-scheme 'prefer-dark'
```

## 📝 Notas

08:00 → modo claro <br>
19:00 → modo oscuro

`DISPLAY=:0` y `DBUS_SESSION_BUS_ADDRESS` apuntan a la sesión gráfica activa

Puedes verificar los valores correctos con:
```bash
echo $DISPLAY
echo $DBUS_SESSION_BUS_ADDRESS
```
