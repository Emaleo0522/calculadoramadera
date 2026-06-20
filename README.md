# Calculadora de Precios — Corte Láser MDF

Calculadora web para presupuestar trabajos de corte/grabado láser en MDF. Calcula el costo (material + mano de obra + luz) y le aplica un margen para obtener el precio de venta. Archivo HTML único, sin dependencias.

**En vivo:** https://calculadoramadera.vercel.app/

## Cómo se calcula el precio

El **Coste Total** es la suma de tres componentes:

| Componente | Fórmula | Significado |
|---|---|---|
| **R1 — Material** | `altura(cm) × ancho(cm) × 0.8735` | Costo del MDF a **$0,8735 por cm²** |
| **R2 — Mano de obra** | `(tiempo_min / 60) × 4000` | **$4000 por hora** de trabajo |
| **R3 — Luz** | `(72 × tiempo_min / 60 / 1000) × 244.2376` | Consumo de la máquina (**72W**) × tarifa (**$244,2376/kWh**) |

`Coste Total = R1 + R2 + R3`

Luego se aplica el margen elegido (al por mayor / al por menor):
`Precio = Coste Total × (1 + porcentaje/100)`

El **tiempo** se ingresa en dos casillas (minutos y segundos) tal como lo muestra el programa de corte, y se combina como `tiempo_min = min + seg/60`.

## Parámetros de costo (actualizar cuando cambien)

Todos viven en el `<script>` de [`index.html`](index.html). Para actualizarlos, editar el número correspondiente:

| Parámetro | Valor actual | Dónde | Cómo se obtiene |
|---|---|---|---|
| Costo MDF por cm² | `0.8735` | `resultado1` | costo total de la plancha ÷ área en cm² (ej: $41.562,50 ÷ 47.580 cm² de una plancha 1,83×2,60 m) |
| Precio mano de obra | `4000` | `resultado2` | tarifa horaria de trabajo |
| Potencia máquina (W) | `72` | `calculo1` | fuente real del láser (Creality Falcon 10W: 24V × 3A = 72W). **No** confundir con los "10W" ópticos del láser |
| Tarifa luz ($/kWh) | `244.2376` | `resultado3` | Cargo Variable de la factura de Edemsa (precio unitario por kWh) |

> **Última actualización de costos:** junio 2026.

## Stack

- HTML5 + CSS3 + JavaScript vanilla (un solo archivo)
- Sin frameworks ni dependencias
- Deploy automático en Vercel desde `main`
