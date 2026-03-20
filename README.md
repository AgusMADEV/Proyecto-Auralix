<div align="center">

# 🎬 Auralix

**Reproductor multimedia inteligente con análisis de sesiones en tiempo real**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.x-000?logo=flask)](https://flask.palletsprojects.com)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?logo=sqlite&logoColor=white)](https://sqlite.org)
[![HTML5](https://img.shields.io/badge/HTML5_Media_API-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement)
[![Status](https://img.shields.io/badge/Status-Production-brightgreen)]()

_Experimenta el poder de la HTML5 Media API con controles personalizados, telemetría avanzada y un sistema de análisis completo_

</div>

---

## 📋 Índice

- [Descripción](#-descripción)
- [Características](#-características)
- [Subida de archivos locales](#-subida-de-archivos-locales)
- [Arquitectura](#-arquitectura)
- [Stack tecnológico](#-stack-tecnológico)
- [Instalación](#-instalación)
- [Uso](#-uso)
- [API REST](#-api-rest)
- [Controles de teclado](#-controles-de-teclado)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Contexto académico](#-contexto-académico)
- [Autor](#-autor)

---

## 🎯 Descripción

**Auralix** es un reproductor multimedia web de nueva generación que combina la potencia de la HTML5 Media API con un sistema completo de análisis y gestión de sesiones. Diseñado como una solución full-stack, Auralix no solo reproduce contenido multimedia, sino que registra, analiza y visualiza cada interacción del usuario.

### ¿Qué hace especial a Auralix?

- **🎮 Controles totalmente personalizados** — Interfaz diseñada desde cero sin usar los controles nativos del navegador
- **📤 Gestión de medios local** — Sube tus propios archivos mediante drag & drop o selección directa
- **📊 Telemetría en tiempo real** — Registra cada acción: play, pause, seek, cambios de velocidad y volumen
- **🎯 Sistema de sesiones** — Cada reproducción genera una sesión completa con métricas de completitud
- **📈 Analytics incorporado** — Visualiza KPIs, rankings de operadores y históricos de reproducción
- **🌓 Experiencia adaptativa** — Tema claro/oscuro con persistencia y diseño responsive

### 💭 La filosofía detrás de Auralix

Auralix nace de la idea de que los reproductores multimedia pueden ser mucho más que simples interfaces de play/pause. Al integrar un sistema completo de telemetría y análisis, cada reproducción se convierte en una fuente valiosa de información sobre patrones de uso, preferencias y comportamiento del usuario.

**El nombre "Auralix"** combina "Aura" (el ambiente único que cada medio genera) y "lix" (sufijo que evoca fluidez y experiencia moderna), representando la experiencia envolvente que buscamos crear.

---

## ✨ Características

### Core

| Módulo                       | Descripción                                                     |
| ---------------------------- | --------------------------------------------------------------- |
| 🎵 **HTML5 Media API**       | `<video>` y `<audio>` nativos sin plugins                       |
| 🎛 **Controles custom**      | Play, Pause, Stop, ±10s, Velocidad (0.75x-1.5x), Volumen        |
| 📊 **Barra progreso custom** | Click-to-seek sobre `<div>` con relleno animado                 |
| 📡 **Telemetría**            | Cada evento registrado con sesión, tipo, posición y payload     |
| 🏆 **Ranking**               | Leaderboard con JOIN + GROUP BY + COALESCE                      |
| 📂 **Biblioteca dinámica**   | Alta por URL o subida local                                     |
| 📤 **Upload local**          | Drag & drop o file picker — MP3, WAV, OGG, FLAC, MP4, WEBM, MOV |

### 14 Mejoras Design System v2

| #   | Mejora                                                                 | Estado |
| --- | ---------------------------------------------------------------------- | ------ |
| 1   | 🎨 **Custom Properties** — 30+ variables CSS (paleta, radios, sombras) | ✅     |
| 2   | 🌓 **Tema claro/oscuro** — Toggle persistente con localStorage         | ✅     |
| 3   | 🟢 **LED reprodución** — Dot animado con pulse durante playback        | ✅     |
| 4   | 📊 **Barra progreso custom** — Div click-to-seek con relleno           | ✅     |
| 5   | 🎵 **Badges de tipo** — audio (azul) / video (púrpura)                 | ✅     |
| 6   | ✔️ **Badges completado** — ✔ Sí / ✘ No en historial                    | ✅     |
| 7   | 🥇 **Badges ranking** — Oro/plata/bronce para top 3                    | ✅     |
| 8   | 🔔 **Sistema toasts** — ok/info/warning/danger                         | ✅     |
| 9   | ⌨️ **Atajos teclado** — Space, flechas (seek ±5s, vol ±5%)             | ✅     |
| 10  | 🌱 **Seed datos demo** — Operadores + sesiones aleatorias              | ✅     |
| 11  | 📥 **Exportación JSON** — Blob download con medios y stats             | ✅     |
| 12  | 📤 **Importación JSON** — File upload + POST /api/import               | ✅     |
| 13  | ✨ **Animaciones CSS** — fadeIn, scaleIn, toastUp, pulse               | ✅     |
| 14  | 📐 **Responsive** — Breakpoints 1024px + 600px                         | ✅     |

---

## 📁 Subida de archivos locales

La aplicación permite subir música y vídeos directamente desde el ordenador:

- **Drag & drop** — Arrastra archivos sobre la zona de subida
- **Selector de archivos** — Click para abrir el explorador de archivos
- **Barra de progreso** — XMLHttpRequest con evento `progress` en tiempo real
- **Formatos soportados:** MP3, WAV, OGG, FLAC, AAC, M4A, WMA, MP4, WEBM, MKV, AVI, MOV, OGV
- **Tamaño máximo:** 100 MB por archivo
- **Auto-detección:** El sistema detecta automáticamente si es audio o vídeo por la extensión

Los archivos se guardan en `static/uploads/` con nombre UUID seguro y se registran en la base de datos.

---

## 🏗 Arquitectura

```
┌────────────────────────────────────┐
│  Frontend (SPA)                    │
│  index.html + app.js + styles.css  │
│                                    │
│  ┌──────────────────────────────┐  │
│  │  HTML5 <video> / <audio>    │  │
│  │  Custom controls + events   │  │
│  │  Upload zone (drag & drop)  │  │
│  └────────────┬─────────────────┘  │
│               │ fetch / XHR        │
├───────────────┼────────────────────┤
│  Backend (Flask · Port 5070)       │
│  app.py + SQLite                   │
│                                    │
│  /api/operators/register           │
│  /api/media (GET/POST)             │
│  /api/upload (multipart file)      │
│  /api/sessions/start|event|end     │
│  /api/leaderboard · /api/stats     │
│  /api/seed · /api/import           │
│                                    │
│  ┌──────────────────────────────┐  │
│  │  SQLite (4 tablas)          │  │
│  │  operators · media_items    │  │
│  │  playback_sessions          │  │
│  │  playback_events            │  │
│  └──────────────────────────────┘  │
└────────────────────────────────────┘
```

---

## 🛠 Stack tecnológico

| Capa          | Tecnología                                               |
| ------------- | -------------------------------------------------------- |
| Backend       | Python 3.10+ · Flask 3.x                                 |
| Base de datos | SQLite 3 (file-based)                                    |
| Frontend      | HTML5 Media API · CSS3 · Vanilla JavaScript ES6+         |
| UX            | Custom Properties · CSS Grid · Animaciones · Drag & Drop |
| Upload        | XMLHttpRequest con progress tracking                     |

---

## 🚀 Instalación

```bash
# 1. Clonar repositorio
git clone https://github.com/agusmadev/Auralix.git
cd Auralix

# 2. Crear entorno virtual
# En Linux/Mac:
python3 -m venv .venv
source .venv/bin/activate

# En Windows:
python -m venv .venv
.venv\Scripts\Activate.ps1

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Ejecutar la aplicación
python app.py
```

📱 Abrir → **http://localhost:5070**

> 💡 **Nota**: La base de datos SQLite (`auralix.sqlite3`) y los datos de ejemplo se generan automáticamente en el primer inicio.

---

## 📖 Uso

### 🚀 Inicio rápido

1. **👤 Regístrate como operador** — Ingresa tu nombre + DNI para comenzar  
2. **📁 Construye tu biblioteca** — Añade medios por URL o arrastra archivos locales (MP3, MP4, WEBM...)  
3. **▶️ Reproduce contenido** — Carga cualquier medio y utiliza los controles personalizados  
4. **⌨️ Atajos de teclado** — `Space` (play/pause), `←→` (seek ±5s), `↑↓` (volumen)  
5. **🎨 Personaliza tu experiencia** — Botón 🌙 para cambiar entre tema claro/oscuro  
6. **📊 Monitorea tu actividad** — Panel lateral con KPIs en tiempo real, ranking y tu historial

### 💡 Características destacadas

- **Drag & Drop inteligente**: Simplemente arrastra archivos multimedia sobre la zona de subida
- **Progreso en tiempo real**: Barra de progreso visual durante la subida de archivos
- **Click-to-seek**: Haz click en cualquier punto de la barra de progreso para saltar
- **Sistema de rankings**: Compite con otros operadores por el mayor número de reproducciones completas
- **Exportación de datos**: Descarga tu biblioteca y estadísticas en formato JSON

---

## 📡 API REST

| Método | Endpoint                       | Descripción                                          |
| ------ | ------------------------------ | ---------------------------------------------------- |
| `GET`  | `/`                            | Página principal (SPA)                               |
| `POST` | `/api/operators/register`      | Registrar operador `{name, dni}`                     |
| `GET`  | `/api/media?kind=audio\|video` | Listar medios                                        |
| `POST` | `/api/media`                   | Añadir medio por URL `{title, kind, sourceUrl}`      |
| `POST` | `/api/upload`                  | **Subir archivo local** (multipart/form-data)        |
| `POST` | `/api/sessions/start`          | Iniciar sesión `{operatorId, mediaItemId}`           |
| `POST` | `/api/sessions/event`          | Registrar evento `{sessionId, eventType, position}`  |
| `POST` | `/api/sessions/end`            | Cerrar sesión `{sessionId, lastPosition, completed}` |
| `GET`  | `/api/operators/<id>/history`  | Historial sesiones                                   |
| `GET`  | `/api/leaderboard`             | Top 10 operadores                                    |
| `GET`  | `/api/stats`                   | KPIs globales                                        |
| `GET`  | `/api/health`                  | Health check                                         |
| `POST` | `/api/seed`                    | Generar datos demo                                   |
| `POST` | `/api/import`                  | Importar medios JSON                                 |

---

## ⌨️ Controles de teclado

| Tecla     | Acción           |
| --------- | ---------------- |
| `Espacio` | Play / Pause     |
| `←`       | Retroceder 5s    |
| `→`       | Avanzar 5s       |
| `↑`       | Subir volumen 5% |
| `↓`       | Bajar volumen 5% |

---

## 📁 Estructura del proyecto

```
Auralix/
├── app.py                          # Flask backend + SQLite + upload endpoint
├── requirements.txt                # flask>=3.0
├── auralix.sqlite3                 # BD auto-generada
├── templates/
│   └── index.html                  # SPA con player, upload zone, dashboard
├── static/
│   ├── app.js                      # Frontend completo (600+ líneas)
│   ├── styles.css                  # Design System v2
│   └── uploads/                    # Archivos subidos desde el ordenador
├── docs/
│   └── Actividad_*.md
├── Actividad_Auralix_53945291X.md
├── Plantilla_Examen_Auralix.md
└── README.md
```

---

## 🎓 Contexto académico

**Auralix** es un proyecto desarrollado como parte del módulo de **Programación Multimedia y Dispositivos Móviles (PMDM)** en el ciclo de **Desarrollo de Aplicaciones Multiplataforma (DAM2)**.

| Campo          | Valor                                              |
| -------------- | -------------------------------------------------- |
| 📚 Módulo      | PMDM — Programación Multimedia y Dispositivos Móviles |
| 🎓 Ciclo       | DAM2 · Desarrollo de Aplicaciones Multiplataforma |
| 📅 Curso       | 2025 / 2026                                        |
| 📝 Actividad   | 003 · Reproductor Multimedia Personalizado         |
| 🎯 Objetivos   | HTML5 Media API, WebSockets, REST APIs, Persistencia |

### 🏆 Características implementadas

Este proyecto va más allá de los requisitos básicos, implementando un sistema completo de telemetría, analytics en tiempo real, gestión de archivos locales, sistema de temas y exportación/importación de datos.

---

## 👤 Autor

**Agustín Morcillo** · [@agusmadev](https://github.com/agusmadev)  
DAM2 · Desarrollo de Aplicaciones Multiplataforma  
Curso 2025/26

---

<div align="center">

_Desarrollado con ❤️ usando HTML5 Media API + Flask + SQLite_

**[⬆ Volver arriba](#-auralix)**

</div>
