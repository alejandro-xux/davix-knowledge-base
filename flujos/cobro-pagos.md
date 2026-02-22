# Flujo: Cobro de Pagos

## Descripcion

Este flujo describe el proceso para registrar y verificar el cobro de pagos asociados a ventas de servicios de salud. Soporta pagos totales y parciales con multiples metodos de pago.

## Actores involucrados

| Actor | Responsabilidad |
|-------|----------------|
| Cajero | Registra el cobro y entrega el comprobante |
| Supervisor | Verifica y aprueba los cobros registrados |
| Cliente/Paciente | Realiza el pago |

## Precondiciones

- Debe existir una **venta** con saldo pendiente de cobro
- El cajero debe tener una **caja abierta**

## Pasos del flujo

### Paso 1: Identificar operacion pendiente

1. El cajero accede al **Listado de Cobros**
2. Filtra por operaciones pendientes de cobro
3. Selecciona la venta o paquete a cobrar

### Paso 2: Crear nuevo cobro

1. Se abre el formulario de **Nuevo Cobro**
2. Se cargan automaticamente los datos de la operacion:
   - Monto total de la venta
   - Monto ya cobrado (si hay cobros previos)
   - Monto pendiente

### Paso 3: Definir tipo de cobro

| Tipo | Cuando usarlo |
|------|--------------|
| **TOTAL** | El cliente paga la totalidad del saldo pendiente en un solo cobro |
| **PARCIAL** | El cliente paga una parte del saldo; quedara saldo pendiente |

### Paso 4: Registrar detalles de pago

Para cada metodo de pago utilizado, se registra un detalle:

1. **Tipo de cobro:** Efectivo, tarjeta, transferencia, etc.
2. **Monto recibido** en ese metodo
3. **Si es tarjeta:**
   - Tipo de tarjeta (debito/credito, marca)
   - Numero de referencia de la transaccion
4. **Si requiere constancia:**
   - Se adjunta voucher o comprobante de pago

Un cobro puede tener **multiples detalles** (ej: parte efectivo + parte tarjeta).

### Paso 5: Registrar efectivo y vuelto

1. Si el pago incluye efectivo:
   - Se ingresa el **monto recibido**
   - El sistema calcula automaticamente el **vuelto**
2. El vuelto = Efectivo recibido - Monto a cobrar

### Paso 6: Confirmar el cobro

1. Se valida que la suma de detalles cubra el monto del cobro
2. Se registra el cobro en el sistema
3. Se asocia a la caja diaria del cajero
4. Si es el **ultimo cobro**, se marca como "finalizado"

### Paso 7: Vincular documentos

1. Se pueden vincular documentos de venta al cobro:
   - Facturas emitidas
   - Boletas emitidas
   - Notas de credito
2. Esto permite trazabilidad documento-pago

### Paso 8: Verificacion (supervisor)

1. El supervisor accede al cobro registrado
2. Revisa cada detalle de pago
3. Verifica:
   - Montos correctos
   - Vouchers adjuntos
   - Consistencia con la operacion
4. Marca cada detalle como **verificado**
5. El cobro queda aprobado

## Diagrama del flujo

```
[Seleccionar operacion] → [Crear cobro] → [Tipo: TOTAL/PARCIAL]
       ↓
[Registrar detalles de pago] → [Efectivo + vuelto] → [Confirmar]
       ↓
[Vincular documentos] → [Verificacion supervisor] → FIN
```

## Cobros parciales - Ciclo

Cuando una venta se paga en cuotas:

```
Venta ($1,000)
  ├─ Cobro 1: PARCIAL ($400) → Pendiente: $600
  ├─ Cobro 2: PARCIAL ($300) → Pendiente: $300
  └─ Cobro 3: TOTAL ($300) → Ultimo cobro → Pendiente: $0 ✓
```

El sistema lleva control automatico de:
- Cantidad de cobros realizados
- Monto total cobrado
- Monto pendiente

## Postcondiciones

- El cobro queda registrado y asociado a la operacion
- El movimiento se refleja en la caja diaria
- Si es el ultimo cobro, la operacion se marca como pagada
- Los documentos quedan vinculados al cobro

## Excepciones

| Excepcion | Accion |
|-----------|--------|
| Monto insuficiente | El sistema alerta; se puede registrar como cobro parcial |
| Caja no abierta | El sistema impide registrar cobros sin caja activa |
| Cobro anulado | Se genera un movimiento de reversa en la caja |
| Verificacion rechazada | El cobro queda pendiente de correccion |
