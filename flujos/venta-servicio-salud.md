# Flujo: Venta de Servicio de Salud

## Descripcion

Este flujo describe el proceso completo para registrar una venta de servicios de salud, desde la seleccion del paciente hasta la emision del comprobante de pago.

## Actores involucrados

| Actor | Responsabilidad |
|-------|----------------|
| Cajero/Vendedor | Registra la venta, selecciona servicios, emite comprobante |
| Paciente | Persona que recibe el servicio medico |
| Cliente | Persona o empresa que paga por el servicio |

## Precondiciones

- El cajero debe tener una **caja abierta**
- El cajero debe tener un **punto de venta** asignado
- Los **servicios/productos** deben estar registrados en el catalogo
- Las **listas de precios** deben estar configuradas

## Pasos del flujo

### Paso 1: Iniciar nueva venta

1. El cajero accede a la pantalla de **Nueva Venta**
2. El sistema asigna automaticamente el cajero y su punto de venta
3. Se genera un registro de venta en estado **NUEVO**

### Paso 2: Seleccionar paciente

1. El cajero busca al paciente por **nombre o numero de documento**
2. Si el paciente no existe, se puede registrar desde el mismo formulario
3. Se selecciona el **tipo de paciente**: PRIVADO, PARTICULAR, SOAT o CONVENIO
4. Si el tipo es CONVENIO, se selecciona el convenio correspondiente

### Paso 3: Seleccionar cliente para facturacion

1. Se determina si el cliente es **persona natural o empresa**
2. Si es empresa, se activa el switch "Es empresa?"
3. Se busca al cliente por nombre o documento
4. Si no existe, se puede registrar desde el formulario
5. El tipo de cliente determina el **tipo de comprobante**: Boleta (persona) o Factura (empresa)

### Paso 4: Registrar referencia medica (opcional)

1. Se selecciona el tipo de referente: MEDICO, OTRO o SIN REFERENTE
2. Si es MEDICO, se busca en el catalogo de medicos referentes
3. Si es OTRO, se ingresa el nombre del referente manualmente

### Paso 5: Agregar servicios/productos

1. Se buscan servicios o productos en el catalogo
2. Para cada item se indica:
   - Cantidad
   - Precio unitario (segun lista de precios)
   - Descuento individual (si aplica)
   - Impuesto (IGV/ISC)
3. El sistema calcula automaticamente subtotales e impuestos

### Paso 6: Aplicar descuentos globales (si aplica)

1. Se puede aplicar un descuento global por porcentaje o monto fijo
2. El sistema recalcula todos los totales

### Paso 7: Definir forma de pago

1. **Contado:** Se registra el pago en el momento
   - Se ingresa el monto recibido
   - El sistema calcula el vuelto
2. **Credito:** Se definen cuotas de pago
   - Se registra monto de adelanto (opcional)
   - Se crean cuotas con fecha y monto

### Paso 8: Verificar la venta

1. Se ejecuta el proceso de **validacion automatica**
2. El sistema verifica:
   - Consistencia de datos del paciente y cliente
   - Tipo de documento vs tipo de cliente
   - Totales calculados correctamente
   - Datos obligatorios completos
3. La venta pasa a estado **VERIFICADO CORRECTAMENTE** o **VERIFICADO CON ERRORES**
4. Si tiene errores, se corrigen y se vuelve a verificar

### Paso 9: Emitir comprobante

1. Se selecciona el tipo de comprobante (Boleta o Factura)
2. Se selecciona la serie correspondiente
3. Se confirma el cliente de facturacion
4. Se emite el documento y se envia a SUNAT
5. Se genera el PDF del comprobante

### Paso 10: Cerrar la venta

1. Una vez verificada y con comprobante emitido, la venta pasa a estado **CERRADO**
2. Se genera el registro de cobro asociado
3. El movimiento se refleja en la caja diaria

## Diagrama del flujo

```
[Iniciar venta] → [Buscar/registrar paciente] → [Buscar/registrar cliente]
       ↓
[Referencia medica] → [Agregar servicios] → [Descuentos]
       ↓
[Forma de pago] → [Verificar] → ¿Errores?
       ↓                           ↓ Si
      No                    [Corregir errores]
       ↓                           ↓
[Emitir comprobante] → [Cerrar venta] → FIN
```

## Postcondiciones

- La venta queda en estado **CERRADO**
- Se genera un **comprobante electronico** enviado a SUNAT
- Se registra un **cobro** asociado (total o parcial)
- El movimiento se refleja en la **caja diaria**

## Excepciones

| Excepcion | Accion |
|-----------|--------|
| Paciente no encontrado | Se puede registrar un nuevo paciente inline |
| Cliente no encontrado | Se puede registrar un nuevo cliente inline |
| Error de verificacion | Se muestran los errores para correccion manual |
| Venta cancelada | La venta pasa a estado BAJA; si habia admisiones, pasan a BAJA POR VENTA |
