# Cotizaciones pendientes — Fase 1 (estructura física)

> Solo componentes del rack y los contenedores. El BOM electrónico se consolida en la **Fase 8**, tras cerrar las decisiones de las Fases 2 y 3.

**Reglas:**
- Marcar `[x]` cuando se haya cotizado.
- Registrar precio real + URL + fecha de cotización en las columnas "Económico real" / "Profesional real".
- Si un componente cambia de especificación tras la decisión de Fase 2/3, mover el renglón a `Fase 8 — cotizaciones electrónica`.

---

## 1. Estructura del rack

| ✔ | Descripción búsqueda | Cant. | Económico (MXN) | Profesional (MXN) | Proveedor sugerido |
|---|---|---|---|---|---|
| [ ] | Rack metálico 4-5 niveles, ~180×90×45 cm, capacidad ≥ 60 kg/nivel | 1 | _pendiente_ | _pendiente_ | Home Depot MX, MercadoLibre MX (búsqueda: "anaquel metálico 5 niveles 180") |
| [ ] | Niveladores de patas roscados M10 con goma | 4 | _pendiente_ | _pendiente_ | Steren, Home Depot |
| [ ] | Anclaje antivuelco a muro (kit) | 1 | _pendiente_ | _pendiente_ | Home Depot |
| [ ] | Tapete antiderrame plástico para nivel inferior | 1 | _pendiente_ | _pendiente_ | MercadoLibre MX |

## 2. Contenedores de fructificación

| ✔ | Descripción búsqueda | Cant. | Económico (MXN) | Profesional (MXN) | Proveedor sugerido |
|---|---|---|---|---|---|
| [ ] | Tote hermético 50–60 L con tapa cierre clip (HDPE alimenticio) | 3 | _pendiente_ | _pendiente_ | MercadoLibre MX, Home Depot (búsqueda: "caja hermética 60 litros") |
| [ ] | Empaque silicona alimenticia grado FDA, rollo 5 m × 6 mm | 1 | _pendiente_ | _pendiente_ | MercadoLibre MX, AliExpress |
| [ ] | Tyvek 1073B u homólogo microporoso para perforaciones, m² | 1 | _pendiente_ | _pendiente_ | AliExpress, proveedor laboratorio |

## 3. Pasamuros, tornillería y sellado

| ✔ | Descripción búsqueda | Cant. | Económico (MXN) | Profesional (MXN) | Proveedor sugerido |
|---|---|---|---|---|---|
| [ ] | Prensaestopas PG7 (cable 3–6.5 mm) con tuerca y arandela | 12 | _pendiente_ | _pendiente_ | Steren, MercadoLibre (búsqueda: "prensaestopa PG7") |
| [ ] | Prensaestopas PG9 (cable 4–8 mm) | 6 | _pendiente_ | _pendiente_ | Steren |
| [ ] | Prensaestopas PG11 (cable 5–10 mm, manguera humidificador) | 3 | _pendiente_ | _pendiente_ | Steren |
| [ ] | Arandelas EPDM 10–14 mm | 24 | _pendiente_ | _pendiente_ | Ferretería |
| [ ] | Silicona neutra grado alimenticio (cartucho) | 2 | _pendiente_ | _pendiente_ | Home Depot (NO usar silicona ácida) |
| [ ] | Tornillería inoxidable A2 M3×16 y M4×16 (kit) | 1 | _pendiente_ | _pendiente_ | MercadoLibre, Tornimex |

## 4. Herramientas específicas

| ✔ | Descripción búsqueda | Cant. | Económico (MXN) | Profesional (MXN) | Proveedor sugerido | Ya lo tengo |
|---|---|---|---|---|---|---|
| [ ] | Sierra cilíndrica (hole saw) — diámetros a definir en §1.2.1 | 1 set | _pendiente_ | _pendiente_ | Home Depot | [ ] |
| [ ] | Punta cónica abrepasos para HDPE | 1 | _pendiente_ | _pendiente_ | Home Depot | [ ] |
| [ ] | Termómetro IR para mapeo térmico del rack | 1 | _pendiente_ | _pendiente_ | Steren, Truper | [ ] |
| [ ] | Higrómetro de referencia ±2 %HR (para calibración cruzada SHT35) | 1 | _pendiente_ | _pendiente_ | MercadoLibre, Steren | [ ] |
| [ ] | Balanza de precisión 0.1 g, rango 0–3 kg | 1 | _pendiente_ | _pendiente_ | MercadoLibre | [ ] |

---

## Diferido a Fase 8 (no cotizar todavía)

- Sensores: SHT35, MH-Z19B, BH1750, DS18B20 (decisión final tras Fase 2).
- TCA9548A multiplexor I²C (depende de topología elegida en §2.2).
- ESP32-S3 / ESP32-CAM (depende de §3.1).
- Humidificadores ultrasónicos por contenedor.
- Ventiladores 5 V o 12 V para FAE.
- LEDs y drivers para fotoperiodo.
- Raspberry Pi / mini-PC para broker MQTT + TSDB.
- Fuentes, cableado, cajas de derivación.
