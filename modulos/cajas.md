# Cajas

## Descripcion

El modulo de Cajas administra el flujo de efectivo diario. Cada cajero abre su caja al inicio del turno, registra los movimientos de ingreso y salida durante el dia, y cierra la caja al final con una conciliacion de saldos.

## Pantallas

### Mi Caja - Movimientos del dia
- Vista de los movimientos de la caja diaria actual
- Registro de ingresos y salidas
- Balance en tiempo real

### Apertura de caja
- Formulario para abrir la caja del dia
- Registro del monto inicial

### Cierre de caja
- Formulario para cerrar la caja
- Conciliacion del monto final

### Consulta de cajas
- Historial de cajas anteriores
- Resumen de movimientos por periodo

## Campos del formulario

### Apertura de caja (estado = 0)

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Responsable | Selector | Si | Cajero responsable |
| Fecha de apertura | Fecha/Hora | Si | Momento de apertura |
| Monto de apertura | Numero | Si | Monto total inicial |
| Monto efectivo | Numero | Si | Efectivo contado al abrir |
| Observaciones | Texto | Si | Notas de la apertura |

### Cierre de caja (estado = 1)

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Fecha de cierre | Fecha/Hora | Si | Momento de cierre |
| Monto de cierre | Numero | Si | Monto total al cerrar |
| Monto efectivo cierre | Numero | Si | Efectivo contado al cerrar |
| Observaciones cierre | Texto | Si | Notas del cierre |

## Tipos de movimiento

### Ingresos de caja
- Pagos en efectivo de ventas
- Cobros recibidos
- Otros ingresos

### Salidas de caja
- Devoluciones
- Gastos operativos
- Transferencias a otras cajas

### Bajas/Anulaciones
- Movimientos cancelados o corregidos
- Requieren justificacion

## Estados de la caja diaria

| Estado | Codigo | Descripcion |
|--------|--------|-------------|
| Nueva apertura | 0 | Caja pendiente de abrir |
| Abierta (necesita cierre) | 1 | Caja operativa, recibiendo movimientos |
| Cerrada | 2 | Caja cerrada y conciliada |

## Flujo operativo

```
1. APERTURA
   └─ Cajero abre la caja registrando monto inicial
   └─ Fecha y hora se registran automaticamente

2. OPERACION
   └─ Se registran movimientos durante el dia:
      ├─ Ingresos (ventas, cobros)
      ├─ Salidas (devoluciones, gastos)
      └─ Anulaciones si es necesario

3. CIERRE
   └─ Cajero cuenta el efectivo fisico
   └─ Sistema compara contra movimientos registrados
   └─ Se registra observaciones de diferencias
```

## Reglas de negocio

1. **Una caja por responsable por dia:** Cada cajero solo puede tener una caja abierta a la vez.
2. **Apertura obligatoria:** No se pueden registrar cobros sin tener una caja abierta.
3. **Auto-poblado de fecha:** La fecha de apertura y cierre se auto-completa con el momento actual.
4. **Lista de vendedores:** Si el usuario actual no esta en la lista de vendedores, se agrega automaticamente.
5. **Validacion condicional:** Los campos obligatorios cambian segun el estado (apertura vs cierre).
6. **Conciliacion:** Al cerrar, el sistema verifica la coherencia entre monto de apertura + movimientos = monto de cierre.
