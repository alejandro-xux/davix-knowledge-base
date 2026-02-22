# Flujo: Gestion de Caja Diaria

## Descripcion

Este flujo describe el ciclo completo de la caja diaria: apertura al inicio del turno, registro de movimientos durante el dia y cierre con conciliacion al final.

## Actores involucrados

| Actor | Responsabilidad |
|-------|----------------|
| Cajero | Abre la caja, registra movimientos y cierra |
| Supervisor | Revisa el cierre y valida la conciliacion |

## Precondiciones

- El cajero debe estar registrado como **vendedor** en el sistema
- Debe tener un **punto de venta** asignado
- No debe tener otra caja abierta

## Pasos del flujo

### Paso 1: Apertura de caja

1. El cajero accede a **Apertura de Caja**
2. Completa el formulario:

| Campo | Accion |
|-------|--------|
| Responsable | Se selecciona (o auto-asigna el cajero actual) |
| Fecha de apertura | Se auto-completa con fecha/hora actual |
| Monto de apertura | Se ingresa el total inicial (efectivo + otros) |
| Monto efectivo | Se ingresa el efectivo contado fisicamente |
| Observaciones | Notas relevantes de la apertura |

3. Se confirma la apertura
4. La caja pasa a estado **ABIERTA** (estado = 1)

### Paso 2: Operacion durante el dia

Con la caja abierta, se registran los movimientos:

#### Ingresos
- Cobros de ventas en efectivo
- Cobros con tarjeta
- Cobros por transferencia
- Otros ingresos

#### Salidas
- Devoluciones a clientes
- Gastos menores
- Transferencias a otras cajas

#### Anulaciones
- Movimientos que se corrigen o cancelan
- Requieren justificacion

### Paso 3: Consulta de movimientos

1. En la pantalla **Mi Caja** se visualizan todos los movimientos del dia
2. Se puede ver el balance acumulado en tiempo real:
   - Total ingresos
   - Total salidas
   - Saldo esperado

### Paso 4: Cierre de caja

1. El cajero accede a **Cierre de Caja**
2. Cuenta el efectivo fisico en caja
3. Completa el formulario:

| Campo | Accion |
|-------|--------|
| Fecha de cierre | Se auto-completa con fecha/hora actual |
| Monto de cierre | Se ingresa el total final |
| Monto efectivo cierre | Se ingresa el efectivo contado fisicamente |
| Observaciones | Notas del cierre (diferencias, incidencias) |

4. El sistema compara:
   - Monto apertura + Ingresos - Salidas = **Saldo esperado**
   - Saldo esperado vs Monto de cierre declarado
5. Si hay diferencia, se registra en observaciones
6. Se confirma el cierre
7. La caja pasa a estado **CERRADA** (estado = 2)

### Paso 5: Conciliacion

1. El cierre se refleja en el **Resumen de Cierre**
2. El supervisor puede revisar:
   - Detalle de todos los movimientos
   - Balance de ingresos vs egresos
   - Diferencias entre saldo esperado y declarado
3. Se genera el reporte de cierre (PDF/Excel)

## Diagrama del flujo

```
[APERTURA]
  ├─ Responsable + Monto inicial
  └─ Estado: ABIERTA
       ↓
[OPERACION DEL DIA]
  ├─ Registrar ingresos (cobros, ventas)
  ├─ Registrar salidas (devoluciones, gastos)
  └─ Registrar anulaciones
       ↓
[CIERRE]
  ├─ Contar efectivo fisico
  ├─ Registrar monto final
  ├─ Comparar con saldo esperado
  └─ Estado: CERRADA
       ↓
[CONCILIACION]
  ├─ Revision del supervisor
  └─ Generacion de reporte
```

## Calculos automaticos

| Calculo | Formula |
|---------|---------|
| Saldo esperado | Monto apertura + Total ingresos - Total salidas |
| Diferencia | Monto cierre declarado - Saldo esperado |
| Balance neto | Total ingresos - Total egresos |

## Postcondiciones

- La caja queda cerrada y no acepta mas movimientos
- El resumen esta disponible para consulta y auditoria
- Se puede generar reporte PDF del cierre
- Al dia siguiente, el cajero debe abrir una nueva caja

## Excepciones

| Excepcion | Accion |
|-----------|--------|
| Diferencia en cierre | Se registra en observaciones; el supervisor investiga |
| Caja no cerrada al fin del dia | El sistema puede alertar al supervisor |
| Movimiento despues del cierre | No es posible; se debe abrir una nueva caja |
| Cajero no registrado | Se agrega automaticamente a la lista de vendedores |
