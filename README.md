# Auralix

> Reproductor multimedia minimalista con telemetría inteligente. Inspirado en Apple Music, construido con tecnología web moderna.

```bash
Python 3.10+ · Flask 3.x · HTML5 Media API · SQLite
```

## Por qué Auralix

La mayoría de reproductores web usan controles nativos del navegador y no registran datos de uso. **Auralix es diferente**: cada interacción se captura, cada sesión se analiza, cada patrón se descubre.

**El nombre** combina "Aura" (ambiente único) y "lix" (fluidez moderna) — la experiencia envolvente que buscamos crear.

## Características principales

**Diseño minimalista**  
Interfaz inspirada en Apple Music con glassmorphism, navegación por pestañas y controles intuitivos.

**Upload inteligente**  
Arrastra archivos MP3, MP4, WEBM... Sistema de drag & drop con barra de progreso en tiempo real.

**Telemetría completa**  
Cada play, pause, seek, cambio de velocidad o volumen queda registrado con timestamp y posición exacta.

**Analytics en vivo**  
Dashboard con KPIs globales, ranking de operadores más activos y tu historial personal de reproducciones.

**Temas adaptativos**  
Modo claro/oscuro con persistencia en localStorage. Cambia según tu preferencia.

**Atajos de teclado**  
`Space` play/pause · `←→` seek ±5s · `↑↓` volumen · Todo sin tocar el ratón.


## Inicio rápido

```bash
# Clonar el proyecto
git clone https://github.com/agusmadev/Auralix.git
cd Auralix

# Entorno virtual (Windows)
python -m venv .venv
.venv\Scripts\Activate.ps1

# Entorno virtual (Linux/Mac)
python3 -m venv .venv
source .venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar
python app.py
```

Abre **http://localhost:5070** y empieza a reproducir.

## Cómo funciona

**1. Regístrate**  
Ingresa tu nombre y DNI. Tu identidad de operador se guarda y todas tus sesiones quedan vinculadas.

**2. Añade contenido**  
Arrastra archivos multimedia o pega URLs. Soporta MP3, MP4, WEBM, OGG, FLAC y más.

**3. Reproduce**  
Haz clic en cualquier medio. Los controles custom permiten play/pause, seek, velocidad y volumen.

**4. Monitorea**  
Vista Analytics muestra tus estadísticas: sesiones totales, tiempo reproducido, tasa de completitud.

## Arquitectura

```
Frontend (SPA)
├─ HTML5 <video> / <audio>
├─ Custom controls + navigation
├─ Drag & drop upload zone
└─ Real-time analytics dashboard

Backend (Flask)
├─ REST API (operators, media, sessions, events)
├─ File upload handler (multipart/form-data)
└─ SQLite (operators, media_items, sessions, events)
```

La aplicación es una SPA que se comunica con Flask mediante fetch API. Toda la lógica de UI está en JavaScript vanilla, sin frameworks.

## API endpoints

```
POST   /api/operators/register        Registrar operador
GET    /api/media                     Listar medios
POST   /api/media                     Añadir medio por URL
POST   /api/upload                    Subir archivo local
POST   /api/sessions/start            Iniciar sesión de reproducción
POST   /api/sessions/event            Registrar evento (play, pause, seek...)
POST   /api/sessions/end              Finalizar sesión
GET    /api/operators/:id/history     Historial de operador
GET    /api/leaderboard               Top 10 operadores
GET    /api/stats                     KPIs globales
GET    /api/health                    Health check
```

## Stack técnico

**Backend** → Flask 3.x + SQLite 3  
**Frontend** → HTML5 Media API + Vanilla JavaScript ES6+  
**Diseño** → CSS3 Custom Properties + Glassmorphism  
**Upload** → XMLHttpRequest con progress tracking  
**Persistencia** → localStorage para tema y sesión


## Estructura del proyecto

```
Auralix/
├── app.py                   → Flask backend + SQLite + REST API
├── requirements.txt         → flask>=3.0
├── auralix.sqlite3          → Base de datos (auto-generada)
├── templates/
│   └── index.html           → SPA principal
├── static/
│   ├── app.js               → Lógica frontend (navegación, player, telemetría)
│   ├── styles.css           → Design system minimalista
│   └── uploads/             → Archivos multimedia subidos
├── Actividad_Auralix_53945291X.md
├── Plantilla_Examen_Auralix.md
└── README.md
```

## Contexto académico

Proyecto desarrollado para el módulo **Programación Multimedia y Dispositivos Móviles (PMDM)** en DAM2.

- **Módulo:** PMDM — Programación Multimedia y Dispositivos Móviles  
- **Ciclo:** DAM2 — Desarrollo de Aplicaciones Multiplataforma  
- **Curso:** 2025/2026  
- **Actividad:** 003 — Reproductor Multimedia Personalizado

**Objetivos cumplidos:** HTML5 Media API, telemetría de eventos, persistencia con SQLite, upload de archivos, analytics en tiempo real, REST API completa.

---

**Agustín Morcillo** · [@agusmadev](https://github.com/agusmadev)  
DAM2 · Desarrollo de Aplicaciones Multiplataforma

*Construido con HTML5 Media API + Flask + SQLite*
