# Fungui

Sistema integral de cultivo gourmet de hongos con monitoreo IoT, marca comercial y distribución vía Telegram.

Producción doméstico-comercial de hongos gourmet (oyster, lion's mane, shiitake) instrumentada para investigación y operación. El operador realiza el proceso completo desde la preparación del sustrato hasta la distribución directa al consumidor final.

---

## 📍 Estado actual del proyecto

| | |
|---|---|
| **Fase activa** | Fase 1 cerrada — listos para arrancar **Fase 2 (firmware ESP32)** |
| **Branch de trabajo siguiente** | `feature/fase2-firmware-esp32` (se creará desde `dev` al dar arranque) |
| **Bloqueado por** | Decisión de topología I²C (TCA9548A maestro vs. 3 ESP32 esclavos) — pendiente de input del operador |
| **Pendiente paralelo** | Operador cursando capacitación en cultivo → completar `docs/fase1-arquitectura-fisica/pendientes-postcurso.md` |
| **Compras urgentes** | Olla de presión, rack, totes herméticos. Ver `cotizaciones_pendientes.md` |

### Progreso general

```
Fase 1 ✅ Arquitectura física            ████████████████████ 100%
Fase 2 🔜 Firmware ESP32                  ░░░░░░░░░░░░░░░░░░░░   0%
Fase 3 ⏳ Cámaras + time-lapse            ░░░░░░░░░░░░░░░░░░░░   0%
Fase 7a ⏳ Schema SQL unificado           ░░░░░░░░░░░░░░░░░░░░   0%
Fase 8 ⚠ Cotizaciones (parcial)          ████░░░░░░░░░░░░░░░░  20%  (físico listo, electrónica pendiente)
Fase 4 ⏳ Dashboard web                   ░░░░░░░░░░░░░░░░░░░░   0%
Fase 5 ⏳ Marca + landing                 ░░░░░░░░░░░░░░░░░░░░   0%
Fase 6 ⏳ Bot Telegram                    ░░░░░░░░░░░░░░░░░░░░   0%
Fase 7b ⏳ CI/CD + meta-repo              ░░░░░░░░░░░░░░░░░░░░   0%
```

---

## Arquitectura general

```
┌─────────────────────────────────────────────────────────────────────┐
│                        Subsistema físico                            │
│   Rack metálico → 3 contenedores herméticos (cámaras de fructif.)   │
│   + olla de presión + Still Air Box (preparación de sustrato)       │
└────────────────────────────────┬────────────────────────────────────┘
                                 │ telemetría
┌────────────────────────────────▼────────────────────────────────────┐
│                       Subsistema embebido                           │
│   ESP32 + sensores (SHT35, MH-Z19B, BH1750) por contenedor          │
│   + ESP32-CAM time-lapse                                            │
└────────────────────────────────┬────────────────────────────────────┘
                                 │ MQTT
┌────────────────────────────────▼────────────────────────────────────┐
│                       Subsistema de datos                           │
│   Broker MQTT + TSDB (InfluxDB/Timescale) + FastAPI + WebSocket     │
└────────────────────────────────┬────────────────────────────────────┘
                                 │ REST + WS
┌─────────────┬──────────────────┴───────────────┬─────────────────────┐
│             │                                  │                     │
▼             ▼                                  ▼                     ▼
Dashboard   Web pública (marca)            Bot Telegram        CI/CD GitHub
(interno)   con cultivo en vivo            (catálogo + pedidos)  Actions
```

---

## Fases del proyecto

El proyecto está organizado en **8 fases secuenciales** con criterios de aceptación verificables al cierre de cada una.

### Orden de ejecución

> `1 → 2 → 3 → 7a → 8 → 4 → 5 → 6`
>
> El BOM electrónico (Fase 8) se consolida **después** de cerrar firmware (2) y cámaras (3) para evitar re-cotización. El schema unificado (7a) nace junto con la telemetría. Marca (5) precede al bot (6) porque éste reutiliza el catálogo.

### Tabla resumen

| Fase | Título | Estado | Entregable principal |
|------|--------|--------|----------------------|
| **1** | Arquitectura física del rack | ✅ cerrada | `docs/fase1-arquitectura-fisica/` |
| **2** | Sistema embebido de monitoreo (ESP32) | 🔜 siguiente | Firmware ESP32 + esquema cableado |
| **3** | Cámara de monitoreo visual y time-lapse | pendiente | ESP32-CAM + backend FastAPI |
| **7a** | Schema SQL unificado | pendiente | `schema.sql` consumido por dashboard y bot |
| **8** | Cotizaciones y compras (electrónica) | parcial | `cotizaciones_pendientes.md` |
| **4** | Dashboard web de monitoreo | pendiente | React + Vite + Tailwind + docker-compose |
| **5** | Marca comercial y página web de venta | pendiente | Next.js 14 + brand guidelines |
| **6** | Bot y canal de Telegram para venta | pendiente | Derivado de [SmartOne-IPTV](https://github.com/Holatfu/SmartOne-IPTV) |
| **7b** | Integración global + CI/CD | pendiente | Meta-repo + GitHub Actions |

### Fase 1 — Arquitectura física (cerrada)

Documentación técnica paramétrica LaTeX. Incluye:

- Plano dimensionado del rack metálico de 4 niveles.
- Diseño de 3 contenedores herméticos como cámaras de fructificación independientes (perforación, pasamuros, sellado).
- Asignación tentativa de especies con tabla de parámetros ambientales citada (Stamets 2000, Chang & Miles 2004).
- BOM físico con placeholders (sin precios inventados) y `cotizaciones_pendientes.md` para búsquedas en proveedores MX.
- Flujo productivo end-to-end con bifurcación fresco/seco post-cosecha.
- **§1.7 Preparación de sustrato**: olla de presión como autoclave, Still Air Box, grain spawn, ensacado. El operador inocula, no recibe bolsas pre-inoculadas.
- `pendientes-postcurso.md`: parking list de decisiones diferidas al curso de cultivo del operador.

📁 [`docs/fase1-arquitectura-fisica/`](docs/fase1-arquitectura-fisica/)

---

## Estrategia de branches (GitFlow)

```
main  ──●─────────────────●─────────●──   solo recibe merges de hitos mayores
        ↑                 ↑         ↑
        Fase 1            …         release/MVP
                                    
dev   ──●──●───●────●─────●───●─────●──   integración continua
            ↑   ↑   ↑     ↑   ↑
            PR  PR  PR    PR  PR
            ↑   ↑   ↑     ↑   ↑
feature/fase2-...   feature/fase3-...   feature/...
(vida corta, se borran tras merge)
```

### Reglas operativas

| Branch | Propósito | Reglas |
|--------|-----------|--------|
| `main` | Snapshot estable, "publicable". | Solo recibe merges desde `dev` en hitos consolidados. No se commitea directo. |
| `dev` | Integración continua de fases. | Recibe PRs squash-merge desde `feature/*`. |
| `feature/faseN-descripcion` | Trabajo de una fase. | Vida corta. Se crea desde `dev`, se borra tras merge. |
| `feature/<otro>` | Cambios transversales (docs, refactor). | Igual que `feature/faseN-*`. |

### Convención de mensajes de commit

```
tipo(scope): descripción breve

Cuerpo opcional explicando el "por qué".
```

Tipos: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`.
Scope típicos: `fase1`, `fase2`, `firmware`, `dashboard`, `bot`, `bom`, etc.

Ejemplo:
```
docs(fase1): rellenar §1.7 esterilización e inoculación
```

### Ciclo de vida de una fase

```
1. git checkout dev && git pull
2. git checkout -b feature/faseN-descripcion
3. ...trabajo + commits atómicos...
4. git push -u origin feature/faseN-descripcion
5. Abrir PR feature/faseN-* → dev
6. Squash merge cuando los criterios de aceptación pasen
7. Borrar la feature branch (remota y local)
8. git checkout dev && git pull origin dev
```

Cuando varias fases acumulan un hito (por ejemplo: sistema embebido viviente, Fases 2+3+4), se abre **PR `dev → main`** como release.

---

## Reglas transversales del proyecto

- **Idioma:** documentación en español, identificadores en código en inglés.
- **Documentación formal:** LaTeX por fase (entregable). Markdown para READMEs y notas operativas.
- **No saltar fases.** Cada fase cierra con criterios de aceptación verificables.
- **Comprobación recursiva:** ante una decisión técnica con dependencia no resuelta, preguntar antes de asumir.
- **Sin precios inventados:** todo componente sin cotización real entra como `[COTIZAR: ...]`.
- **Commits atómicos** con convención `tipo(scope): descripción`.
- **Tests** para drivers de sensores y endpoints críticos del backend (Fases 2 y 4 en adelante).
- **Trade-offs arquitectónicos:** se presentan 2–3 opciones con pros/contras antes de decidir.

---

## Estructura del repo (objetivo)

```
Fungui/
├── README.md                          ← este archivo
├── docs/
│   ├── fase1-arquitectura-fisica/     ✅
│   ├── fase2-firmware-embebido/       🔜
│   ├── fase3-camaras-timelapse/
│   ├── fase4-dashboard/
│   ├── fase5-marca-web/
│   ├── fase6-bot-telegram/
│   └── fase7-integracion-global/
├── firmware/
│   └── esp32-master/                  ← Fase 2
├── camara/                            ← Fase 3
├── dashboard/                         ← Fase 4
├── marca-web/                         ← Fase 5
├── tienda-telegram-hongos/            ← Fase 6
├── schema/
│   └── schema.sql                     ← Fase 7
└── .github/
    └── workflows/                     ← CI/CD Fase 7
```

Cada subdirectorio mantiene su propio `README.md` operativo.

---

## Stack tecnológico

| Capa | Tecnología | Justificación |
|------|------------|---------------|
| Microcontrolador | ESP32-S3 / ESP32 | WiFi nativo, soporte cámara, ecosistema PlatformIO. |
| Sensores | SHT35, MH-Z19B, BH1750, DS18B20 | Precisión documentada, drivers maduros. |
| Comunicación | MQTT (Mosquitto) | Latencia baja, topics jerárquicos, broker local. |
| TSDB | InfluxDB o TimescaleDB | A decidir en Fase 2/4 con justificación. |
| Backend | FastAPI (Python) | Pythonic, async, integración natural con MQTT. |
| Dashboard | React + Vite + Tailwind + Recharts | Stack moderno, componentes shadcn/ui. |
| Marca web | Next.js 14 (App Router) + Tailwind | SSR para SEO, Vercel deploy gratis. |
| Bot | python-telegram-bot v20+ o aiogram v3 | Decisión: alinear con [SmartOne-IPTV](https://github.com/Holatfu/SmartOne-IPTV). |
| Despliegue | docker-compose en Raspberry Pi 4/5 | Self-hosted, control total. |
| CI/CD | GitHub Actions | Tests automáticos al push. |

---

## Documentación contextual

- 📄 [Fase 1 — Arquitectura física del rack](docs/fase1-arquitectura-fisica/README.md)
- 📋 [Pendientes post-curso](docs/fase1-arquitectura-fisica/pendientes-postcurso.md)
- 💰 [Cotizaciones pendientes](docs/fase1-arquitectura-fisica/cotizaciones_pendientes.md)

---

FF Holatfu
