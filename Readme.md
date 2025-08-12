# MiHUD (Rainmeter)

**MiHUD** es un conjunto modular de skins para Rainmeter diseñado para mostrar información de sistema, red, hora y espectro musical, con un diseño visual personalizable y bordes animados.

---

## 📂 Estructura del proyecto

```
MiHUD/
│  Loader.ini                 # (Opcional) Carga todos los módulos a la vez
│
├─ @Resources/
│  ├─ Variables.inc           # Variables globales (colores, tamaños, tipografía)
│  ├─ Fonts/                  # Fuentes personalizadas
│  ├─ Images/                 # Iconos, texturas, bordes
│  └─ Scripts/                # Lua para animaciones y utilidades
│
├─ Clock/
│  └─ Clock.ini               # Módulo de reloj digital y fecha
│
├─ InfoPanel/
│  └─ InfoPanel.ini           # Panel octagonal con info CPU/RAM/Disco/Hora/Host
│
├─ MusicSpectrum/
│  └─ MusicSpectrum.ini       # Espectro de música (tipo CAVA)
│
└─ Network/
   └─ SpeedNetwork.ini        # IPv4, tipo de conexión e IO de red
```

---

## ⚙️ Instalación y uso

1. Copia la carpeta `MiHUD` en:
   ```
   Documentos\Rainmeter\Skins\
   ```
2. Abre Rainmeter y selecciona **Refresh all**.
3. Carga módulos individuales o `Loader.ini` para todo el HUD.

---

## 🔧 Variables globales (`@Resources/Variables.inc`)

```ini
[Variables]
FontName=Segoe UI
FontSize=12
FontColor=255,255,255,255

FillColor=0,0,0,200
BorderColor=255,0,0,255
BorderWidth=4

PanelWidth=300
PanelHeight=450
CornerCut=25

Bars=48
BarWidth=6
BarGap=3
```

---

## 🛠 Funcionamiento

Cada módulo Rainmeter:
- **Measures** → Obtienen datos del sistema (`CPU`, `RAM`, `NetIn`, `NetOut`, `AudioLevel`, `Time`, `SysInfo`, etc.).
- **Meters** → Dibujan en pantalla (`Shape`, `String`, `Bar`, `Image`) usando las variables globales.
- **Recursos compartidos** → Colores, tamaños y estilos unificados desde `Variables.inc`.

---

### 📜 Diagrama ASCII — Arquitectura

```
+------------------------- Rainmeter Engine --------------------------+
|                                                                     |
|  Measures (datos)                     Meters (render)               |
|  -----------------                    -------------------           |
|  CPU, RAM, Disk, Time, SysInfo  -->   String, Shape, Bar, Image     |
|  NetIn/NetOut, AudioLevel             (usa Variables.inc)           |
|                                                                     |
|  @Resources                                                           |
|   ├─ Variables.inc  -> Colores/Tamaños/Tipografías                   |
|   ├─ Images/       -> Iconos wifi/ethernet, texturas                 |
|   └─ Scripts/      -> Lua (animaciones de bordes, utilidades)        |
+---------------------------------------------------------------------+
             |                    |                     |
             v                    v                     v
        InfoPanel.ini        MusicSpectrum.ini       SpeedNetwork.ini
             |                    |                     |
             v                    v                     v
       Panel sistema         Espectro FFT          IPv4 + IO + icono
```

---

### 🔄 Diagrama ASCII — Ciclo de actualización

```
[Update=16ms (~60 FPS)]
      |
      v
  Measures leen datos
  (CPU, RAM, Disco, Hora,
   SysInfo, Red, Audio)
      |
      v
  Procesamiento:
   - Conversiones de unidades
   - Normalización
   - Cálculos FFT (espectro)
      |
      v
  Meters dibujan:
   - Shapes (octágono/rectángulo)
   - Strings (texto valores)
   - Bars (barras espectro)
   - Images (iconos conexión)
```

---

## 📌 Módulos

- **InfoPanel** → Panel octagonal con CPU, RAM, Disco, Host y Hora.  
- **MusicSpectrum** → Rectángulo con espectro musical FFT.  
- **Clock** → Hora y fecha minimalistas.  
- **Network** → IPv4, tipo de conexión (WiFi/Ethernet) y velocidades de red.  

---

## 🚀 Roadmap

- [ ] Animaciones de bordes tipo “líquido” con gradiente.
- [ ] Temas claros/oscuros.
- [ ] Layouts predefinidos.
- [ ] Tooltips e interacciones extra.

---

## 📜 Licencia

MIT — libre para modificar y compartir.
