# Cierre y Conciliacion

## Descripcion

El modulo de Cierre gestiona la conciliacion financiera periodica. Permite revisar los resumenes de movimientos, validar ingresos contra egresos y generar reportes consolidados.

## Pantallas

### Resumen de cierre
- Lista consolidada de cierres por periodo
- Filtros por rango de fechas, responsable y punto de venta
- Totales de ingresos y egresos

### Detalle de cierre
- Desglose de todos los movimientos incluidos en un cierre
- Separacion de ingresos y egresos
- Identificacion de diferencias

### Movimientos de ingresos y egresos
- Vista detallada de cada movimiento
- Filtrable por tipo, fecha y monto

## Filtros disponibles

| Filtro | Tipo | Descripcion |
|--------|------|-------------|
| Fecha desde | Fecha | Inicio del periodo a consultar |
| Fecha hasta | Fecha | Fin del periodo a consultar |
| Responsable | Selector | Cajero o responsable del cierre |
| Punto de venta | Selector | Ubicacion fisica |
| Tipo de movimiento | Selector | Ingreso o egreso |

## Contenido del resumen

| Dato | Descripcion |
|------|-------------|
| Total ingresos | Suma de todos los cobros y entradas de caja |
| Total egresos | Suma de todas las salidas y devoluciones |
| Balance neto | Diferencia entre ingresos y egresos |
| Cantidad de operaciones | Numero total de movimientos |
| Desglose por metodo de pago | Efectivo, tarjeta, transferencia, etc. |

## Reportes

- **Reporte de caja resumen** - PDF con el consolidado del periodo
- **Exportacion Excel** - Detalle de movimientos en formato descargable

## Reglas de negocio

1. **Dependencia con cajas:** Solo se pueden generar cierres a partir de cajas que ya fueron cerradas.
2. **Periodo definido:** El cierre abarca un rango de fechas especifico.
3. **Inmutabilidad:** Una vez generado, el cierre no puede modificarse; solo se puede generar uno nuevo.
4. **Auditoria:** Todos los movimientos incluidos en el cierre quedan trazados con fecha, responsable y tipo.
