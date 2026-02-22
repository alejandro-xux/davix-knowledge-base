# Cobros

## Descripcion

El modulo de Cobros gestiona la cobranza de las ventas realizadas. Permite registrar pagos totales o parciales, verificar su validez y vincular documentos de soporte. Se integra directamente con el modulo de Cajas para el flujo financiero.

## Pantallas

### Listado de cobros
- Tabla con todos los cobros registrados
- Filtros por fecha, estado, tipo de operacion
- Acciones: ver detalle, verificar, anular

### Nuevo cobro
- Formulario para registrar un pago contra una venta
- Seleccion de la venta asociada
- Registro de montos y metodos de pago

### Detalle de cobro (solo lectura)
- Vista de consulta con toda la informacion del cobro
- Documentos asociados y detalles de pago

## Campos del formulario de cobro

### Datos generales

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Serie | Texto | No | Serie del documento de cobro |
| Numero | Texto | No | Numero del cobro |
| Fecha | Fecha | No | Fecha del cobro (default: hoy) |
| Tipo de operacion | Selector | No | VENTA, CUENTA o PAQUETE |
| Tipo | Selector | No | TOTAL o PARCIAL |
| Ultimo cobro | Switch | No | Indica si es el ultimo pago pendiente |

### Datos financieros

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Monto | Numero | No | Monto del cobro actual |
| Monto total | Numero | No | Monto total de la operacion |
| Monto efectivo recibido | Numero | No | Efectivo recibido del cliente |
| Monto efectivo vuelto | Numero | No | Vuelto calculado automaticamente |
| Monto cobrado | Numero | Auto | Total acumulado de cobros anteriores |
| Monto pendiente | Numero | Auto | Saldo pendiente de cobro |
| Cantidad total cobros | Numero | Auto | Numero de cobros realizados |

### Datos de referencia

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Operacion referencia | Selector | No | Venta o paquete asociado |
| Responsable | Selector | No | Persona responsable del cobro |
| Caja | Selector | No | Caja donde se registra el cobro |
| Codigo de grupo | Texto | No | Agrupador de cobros relacionados |

## Tipos de operacion

| Tipo | Descripcion |
|------|-------------|
| VENTA | Cobro asociado a una venta de servicio de salud |
| CUENTA | Cobro de cuentas por cobrar |
| PAQUETE | Cobro de paquetes de servicios |

## Tipos de cobro

| Tipo | Descripcion |
|------|-------------|
| TOTAL | Pago completo del monto adeudado en un solo cobro |
| PARCIAL | Pago fraccionado, permite multiples cobros hasta completar |

## Detalles de pago

Cada cobro puede tener multiples detalles con diferentes metodos de pago:

| Campo | Tipo | Descripcion |
|-------|------|-------------|
| Tipo de cobro | Selector | Metodo de pago (efectivo, tarjeta, transferencia, etc.) |
| Fecha | Fecha | Fecha del pago especifico |
| Tipo de tarjeta | Selector | Solo si pago con tarjeta |
| Numero de referencia | Texto | Referencia de transaccion bancaria |
| Verificado | Switch | Indica si el pago fue verificado |
| Monto recibido | Numero | Monto de este detalle |
| Voucher | Archivo | Constancia/comprobante adjunto |

## Documentos asociados

Un cobro puede vincular documentos de venta emitidos:
- Facturas
- Boletas
- Notas de credito
- Constancias de pago

## Flujo de verificacion

1. Se registra el cobro con sus detalles
2. El supervisor puede verificar cada detalle de pago
3. Se valida que los montos coincidan
4. Se marca como verificado o se rechaza

## Reglas de negocio

1. **Vuelto automatico:** El sistema calcula automaticamente el vuelto cuando el efectivo recibido supera el monto a cobrar.
2. **Cobros parciales:** Cuando el tipo es PARCIAL, el sistema lleva control del saldo pendiente y la cantidad de cobros realizados.
3. **Ultimo cobro:** Cuando se marca como "ultimo cobro", el sistema finaliza el ciclo de cobranza de esa operacion.
4. **Vinculacion con caja:** Todo cobro se registra en la caja diaria del responsable.
5. **Verificacion obligatoria:** Los cobros deben ser verificados antes de considerarse definitivos.
6. **Precision decimal:** Los montos se manejan con 2 decimales.
