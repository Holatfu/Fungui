# Pendientes post-curso

> Decisiones e información que el operador completará **después de tomar el curso de cultivo**. Cada renglón es accionable: el ítem se cierra cuando el campo correspondiente del LaTeX o de la base de datos deja de tener el placeholder `[POST-CURSO: ...]`.

Convenciones:
- `[ ]` pendiente · `[x]` completado.
- Referencia entre paréntesis al archivo o sección afectado.

---

## A. Selección de especies

- [ ] **Confirmar o modificar las tres especies asumidas** (oyster, lion's mane, shiitake). (`params.tex` → `\paramEspecieA/B/C`, `secciones/03-asignacion-especies.tex`)
- [ ] **Cultivo madre por especie**: decidir si se compra jeringa de esporas, jeringa de cultivo líquido (LC) o se trabaja desde placa propia. (`secciones/04-bom.tex` §1.4.5, `secciones/07-preparacion-sustrato.tex` §1.7.3)
- [ ] **Proveedor de cultivo madre en MX**: identificar al menos dos opciones confiables. (`cotizaciones_pendientes.md`)
- [ ] **Validar parámetros ambientales por especie** contra el material del curso vs. la tabla de literatura. (`secciones/03-asignacion-especies.tex` tabla 1)
- [ ] **Cold shock para shiitake**: confirmar duración y temperatura recomendadas por el instructor. (`secciones/03-asignacion-especies.tex` notas operativas)

## B. Sustrato

- [ ] **Sustrato específico por especie** (paja, pellets, granos suplementados, fórmula maestra del curso). (`secciones/07-preparacion-sustrato.tex` §1.7.4, `secciones/04-bom.tex` §1.4.5)
- [ ] **Relación de hidratación** (kg agua / kg sustrato seco) para alcanzar HR ≈ 65 %. (`secciones/07-preparacion-sustrato.tex`)
- [ ] **% de spawn sobre masa húmeda** (rango actual 5–10 %, definir target del curso). (`secciones/07-preparacion-sustrato.tex`)
- [ ] **Suplementación** (yeso CaSO₄, salvado, harina de soya) en qué % y para qué especie. (`secciones/04-bom.tex`)

## C. Esterilización

- [ ] **Validar tiempo de esterilización** según volumen y tipo de carga real. Actual: 90 min sustrato, 60 min grano @ 15 psi. (`secciones/07-preparacion-sustrato.tex` tabla 4)
- [ ] **Decidir si la olla doméstica 23 L es suficiente** o requiere upgrade a olla industrial / autoclave de 40 L+. Depende del tamaño de lote objetivo. (`params.tex` → `\paramVolOllaPresion`, `cotizaciones_pendientes.md`)
- [ ] **Termómetro independiente** para verificación de ciclo: marca y modelo. (`secciones/04-bom.tex`)

## D. Still Air Box / cabina de flujo

- [ ] **Tamaño exacto del SAB** según ergonomía del operador. (`secciones/07-preparacion-sustrato.tex` §1.7.2)
- [ ] **Decidir si se migra a flow hood HEPA** desde el inicio o tras 5 lotes con > 10 % contaminación. (`secciones/07-preparacion-sustrato.tex`)

## E. Deshidratadora

- [ ] **Marca y modelo del equipo del operador**. (`secciones/06-postcosecha.tex` §1.6.1)
- [ ] **Potencia eléctrica [W]**, número y área de bandejas, rango térmico, tipo de flujo. (`secciones/06-postcosecha.tex`)
- [ ] **Validar tabla 3 (parámetros de secado)** contra recomendación del fabricante de la deshidratadora. (`secciones/06-postcosecha.tex` §1.6.2)
- [ ] **Caracterizar curva propia**: llenar `plantilla-secado.csv` tras 3 lotes por especie.

## F. Rack y contenedores

- [ ] **Restricciones físicas reales del espacio**: actualizar `params.tex` con `\paramHmax`, `\paramWmax`, `\paramDmax` reales si difieren de los defaults comerciales.
- [ ] **Mapeo térmico del rack en sitio** antes de cargar lotes (termómetro IR + datalogger 24 h). Usar para validar asignación de §1.3. (`secciones/03-asignacion-especies.tex` § asignación)
- [ ] **Volumen real de tote disponible en MX** (a veces sólo hay 50 L o 70 L, no 55 L exacto). (`params.tex` → `\paramVolTote`)

## G. Regulatorio y comercial (fuera de alcance Fase 1, parking)

- [ ] **Etiquetado NOM-051** para producto deshidratado.
- [ ] **Registro sanitario COFEPRIS** (modalidad y costo).
- [ ] **Trazabilidad de lote** (formato de código y QR opcional).

## H. Cotizaciones pendientes (cross-link)

Todas las cotizaciones siguen vivas en `cotizaciones_pendientes.md`. Cuando una decisión post-curso elimine o cambie un componente, mover el renglón de un archivo al otro.
