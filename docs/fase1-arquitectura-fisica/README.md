# Fase 1 — Arquitectura física del rack de producción

Documentación técnica del subsistema físico: rack, contenedores, flujo
productivo y post-cosecha con deshidratadora.

**Estado actual:** esqueleto (revisión `0.1-esqueleto`). Las secciones
contienen únicamente la estructura y los `TODO` que marcan qué se
rellenará tras validación.

---

## Estructura del directorio

```
fase1-arquitectura-fisica/
├── main.tex                       # documento maestro LaTeX
├── params.tex                     # parámetros editables (H, W, D, T_amb, ...)
├── referencias.bib                # bibliografía (vacía, con plantillas)
├── secciones/
│   ├── 01-rack.tex
│   ├── 02-contenedores.tex
│   ├── 03-asignacion-especies.tex
│   ├── 04-bom.tex
│   ├── 05-flujo-productivo.tex
│   └── 06-postcosecha.tex
├── diagramas/
│   ├── flujo-productivo.mmd       # mermaid
│   └── flujo-postcosecha.mmd      # mermaid con bifurcación fresco/seco
├── plantilla-secado.csv           # caracterización experimental vacía
├── cotizaciones_pendientes.md     # BOM físico con placeholders
└── README.md                      # este archivo
```

---

## Cómo compilar el LaTeX

Requiere TeX Live completo (o MiKTeX) con `latexmk`, `biber`,
paquetes `tikz`, `siunitx`, `biblatex`, `babel-spanish`.

```bash
cd docs/fase1-arquitectura-fisica
latexmk -pdf main.tex
```

Limpieza:

```bash
latexmk -C
```

## Cómo renderizar los diagramas mermaid

```bash
# Instalación (una vez):
npm install -g @mermaid-js/mermaid-cli

# Render:
mmdc -i diagramas/flujo-productivo.mmd   -o diagramas/flujo-productivo.png
mmdc -i diagramas/flujo-postcosecha.mmd  -o diagramas/flujo-postcosecha.png
```

GitHub renderiza los `.mmd` directamente cuando se embeben en
markdown; el PNG sólo es necesario para incluirlos en el LaTeX
mientras no estén redibujados en TikZ.

---

## Parámetros editables

Editar `params.tex` para adaptar el documento a tus restricciones
reales. Los defaults actuales corresponden a un rack comercial típico:

| Macro                    | Default | Significado                        |
|--------------------------|---------|------------------------------------|
| `\paramHmax`             | 180 cm  | Altura máxima disponible           |
| `\paramWmax`             | 90 cm   | Ancho máximo disponible            |
| `\paramDmax`             | 45 cm   | Fondo máximo disponible            |
| `\paramTambMin`          | 16 °C   | T ambiente mínima esperada         |
| `\paramTambMax`          | 26 °C   | T ambiente máxima esperada         |
| `\paramHRamb`            | 45 %    | HR ambiente típica                 |
| `\paramNiveles`          | 4       | Número de niveles del rack         |
| `\paramNcontenedores`    | 3       | Número de cámaras de fructificación|
| `\paramVolTote`          | 55 L    | Volumen nominal de cada tote       |

---

## Qué validar antes de pasar a Fase 2

Checklist de aceptación del **esqueleto**:

- [ ] El árbol de archivos refleja 1:1 las secciones 1.1–1.6 del brief.
- [ ] `params.tex` cubre las variables que esperas como entrada.
- [ ] Los dos diagramas mermaid representan correctamente los flujos
      productivo y post-cosecha.
- [ ] `cotizaciones_pendientes.md` cubre todos los componentes
      **físicos** (no electrónicos: esos son Fase 8).
- [ ] `plantilla-secado.csv` tiene las columnas que esperas registrar
      por lote.
- [ ] La bibliografía `.bib` referencia las fuentes mínimas que quieres
      sostener para §1.3 y §1.6.

Una vez validado el esqueleto, se procede sección por sección:
**§1.1 → §1.2 → §1.3 → §1.4 → §1.5 → §1.6**.

En cada bloque, antes de redactar, te preguntaré las decisiones que
no estén implícitas en `params.tex` (p. ej. material exacto del rack,
diámetro de perforación por especie, especificaciones de la
deshidratadora).
