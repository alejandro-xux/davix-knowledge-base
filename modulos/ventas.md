# Ventas

## Descripcion

El modulo de Ventas permite registrar, verificar y cerrar transacciones de venta de servicios y productos de salud. Es el nucleo del Sistema de Gestion Comercial y se conecta con admisiones, cobros, facturacion y caja.

## Pantallas

### Listado de ventas
- Vista principal con tabla de todas las ventas registradas
- Filtros por fecha, estado, vendedor y punto de venta
- Acciones: ver detalle, verificar, dar de baja
- Exportacion a Excel

### Nueva venta
- Formulario completo para registrar una transaccion de venta
- Asociacion de paciente, cliente y medico referente
- Seleccion de servicios/productos con precios
- Calculo automatico de impuestos y descuentos

## Campos del formulario de venta

### Datos del vendedor

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Cajero(a) | Selector | No | Vendedor/cajero asignado a la venta |
| Punto de venta | Selector | No | Ubicacion fisica donde se realiza la venta |

### Datos del paciente/cliente

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Es empresa? | Switch | No | Indica si el cliente es persona natural o empresa |
| Paciente | Buscador | Si | Buscar por nombres o numero de documento |
| Tipo paciente | Selector | Si | PRIVADO, PARTICULAR, SOAT o CONVENIO |
| Cliente | Buscador | Si | Cliente para facturacion |
| Convenio | Selector | Condicional | Solo si tipo paciente = CONVENIO |

### Datos de referencia medica

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Tipo referente | Selector | No | MEDICO, OTRO o SIN REFERENTE |
| Medico referente | Buscador | Condicional | Obligatorio si tipo referente = MEDICO |
| Referente | Texto | Condicional | Obligatorio si tipo referente = OTRO |

### Datos del documento

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Tipo de documento | Selector | Si | BOLETA (3) o FACTURA (1) |
| Serie | Texto | No | Serie del comprobante (auto-generada) |
| Numero | Texto | No | Numero correlativo (auto-generado) |
| Fecha | Fecha | Si | Fecha de la transaccion |
| Moneda | Selector | No | SOLES (1) o DOLARES (2) |
| Fecha de entrega | Fecha | No | Fecha estimada de entrega |

### Datos financieros

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Lista de precios | Selector | Si | Lista de precios aplicable |
| Descuento global tipo | Selector | Si | PORCENTAJE o MONTO fijo |
| Descuento global valor | Numero | Si | Valor del descuento |
| Forma de pago | Selector | No | CONTADO o CREDITO |
| Monto adelanto | Numero | No | Pago anticipado (solo para credito) |
| Observacion | Texto | Si | Notas adicionales |

### Detalle de productos/servicios

Cada linea de detalle incluye:
- Producto o servicio seleccionado
- Cantidad
- Precio unitario
- Descuento por item
- Impuesto aplicable (IGV, ISC)
- Subtotal calculado

### Totales calculados automaticamente

| Campo | Descripcion |
|-------|-------------|
| Total cantidad | Suma de unidades vendidas |
| Total valor venta | Subtotal antes de impuestos |
| Total impuestos | Suma de IGV + ISC |
| Total descuentos | Suma de descuentos aplicados |
| Operaciones gravadas | Base imponible con IGV |
| Operaciones exoneradas | Monto exonerado de IGV |
| Operaciones inafectas | Monto no afecto a IGV |
| Operaciones gratuitas | Monto de items gratuitos |
| Monto total | Total final a pagar |

### Cuotas de pago (solo para credito)

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Orden | Numero | Auto | Numero de cuota |
| Fecha | Fecha | Si | Fecha de vencimiento |
| Monto | Numero | Si | Monto de la cuota |
| Moneda | Texto | Auto | PEN por defecto |

## Estados de una venta

| Estado | Codigo | Color | Descripcion |
|--------|--------|-------|-------------|
| Nuevo | 0 | Azul (info) | Venta recien creada |
| Verificado con errores | 1 | Rojo (error) | Se verifico y tiene inconsistencias |
| Verificado correctamente | 2 | Amarillo (warning) | Verificacion exitosa, pendiente de cierre |
| Cerrado | 3 | Verde (success) | Venta completada y cerrada |
| Baja | 4 | Rojo (error) | Venta cancelada |
| Sin verificar | 5 | Gris (neutral) | Aun no se ha ejecutado verificacion |

### Diagrama de transiciones

```
NUEVO → VERIFICADO CON ERRORES → (corregir) → VERIFICADO CORRECTAMENTE → CERRADO
NUEVO → SIN VERIFICAR → VERIFICADO CORRECTAMENTE → CERRADO
Cualquier estado → BAJA (cancelacion)
```

## Reglas de negocio

1. **Tipo de documento segun cliente:** Si el cliente es empresa (con RUC), se debe emitir FACTURA. Si es persona natural, se emite BOLETA.
2. **Convenio obligatorio:** Si el tipo de paciente es CONVENIO, se debe seleccionar el convenio correspondiente.
3. **Referente medico:** Si el tipo de referente es MEDICO, se debe seleccionar un medico referente del catalogo.
4. **Precision decimal:** Los calculos financieros usan BigNumber.js con 3 decimales para valores unitarios y 2 decimales para subtotales.
5. **Validacion de cierre:** Una venta debe estar en estado "Verificado correctamente" para poder cerrarse.
6. **Credito:** Si la forma de pago es CREDITO, se deben registrar las cuotas de pago con fechas y montos.
