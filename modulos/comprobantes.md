# Comprobantes

## Descripcion

El modulo de Comprobantes gestiona la emision de documentos tributarios electronicos vinculados a las ventas. Soporta facturas, boletas, notas de credito y guias de remision, con integracion directa con SUNAT.

## Tipos de comprobante

| Tipo | Codigo | Descripcion | Destinatario |
|------|--------|-------------|--------------|
| Factura | 1 | Comprobante para empresas con RUC | Persona juridica |
| Boleta | 3 | Comprobante para personas naturales | Persona natural |
| Nota de credito | 7 | Documento para anulaciones o correcciones | Ambos |
| Guia de remision | 9 | Documento de traslado de bienes | Ambos |

## Campos del formulario de emision

### Datos del documento

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Tipo de documento | Selector | Si | BOLETA (3) o FACTURA (1). Default: BOLETA |
| Serie | Texto | Si | Serie del comprobante (segun tipo) |
| Numero | Texto | No | Numero correlativo (auto-generado) |
| Fecha | Fecha | Si | Fecha de emision |
| Enviar a SUNAT | Switch | No | Indica si se envia electronicamente. Default: Si |

### Datos del vendedor

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Vendedor apellidos | Texto | Auto | Apellidos del cajero emisor |
| Vendedor nombres | Texto | Auto | Nombres del cajero emisor |
| Vendedor alias | Texto | Auto | Alias del cajero |

### Datos del cliente

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Cliente | Buscador | Si | Cliente a quien se emite el documento |

### Detalle de productos/servicios

Cada linea del comprobante incluye:
- Descripcion del servicio o producto
- Cantidad
- Precio unitario
- Impuesto aplicable
- Subtotal

### Totales

| Campo | Descripcion |
|-------|-------------|
| Total valor venta | Subtotal antes de impuestos |
| Total impuestos | Suma de IGV + ISC |
| Total descuentos | Descuentos aplicados |
| Total cantidad | Cantidad de items |
| Monto total | Total a pagar |
| Operaciones gravadas | Base imponible con IGV |
| Operaciones exoneradas | Exonerado de IGV |
| Operaciones inafectas | No afecto a IGV |
| Operaciones gratuitas | Servicios gratuitos |
| Total IGV | Impuesto General a las Ventas |
| Total ISC | Impuesto Selectivo al Consumo |

## Series de comprobantes

Las series se configuran por tipo de documento:

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| SERIE-BOLETA | Configuracion | Series habilitadas para boletas |
| SERIE-FACTURA | Configuracion | Series habilitadas para facturas |

La serie se selecciona al momento de emitir y el numero correlativo se genera automaticamente.

## Impuestos

### IGV (Impuesto General a las Ventas)
- Se calcula como porcentaje sobre el valor de venta
- Aplicable a operaciones gravadas
- El formato de texto es: `CODIGO [PORCENTAJE%] - NOMBRE`

### ISC (Impuesto Selectivo al Consumo)
- Aplica a productos/servicios especificos
- Se calcula por porcentaje o monto fijo

## Reportes generados

| Reporte | Descripcion |
|---------|-------------|
| Documento de venta | PDF del comprobante emitido (factura/boleta) |
| Nota de venta | PDF de la nota de venta interna |
| Nota de credito | PDF de la nota de credito |
| Guia de remision | PDF de la guia de remision |
| Resumen de caja | PDF consolidado de caja |

Los reportes se generan a traves del servicio **Report Factory** (`v2.0.1/erpx/reports/factory/generate`).

## Reglas de negocio

1. **Tipo segun cliente:** Si el cliente tiene RUC (empresa), se debe emitir Factura. Si tiene DNI (persona natural), se emite Boleta.
2. **Serie unica por tipo:** Cada tipo de documento tiene sus propias series configuradas.
3. **Numeracion correlativa:** El numero se genera automaticamente y es correlativo dentro de cada serie.
4. **Envio a SUNAT:** Por defecto, todos los comprobantes se envian electronicamente a SUNAT.
5. **Nota de credito:** Solo se puede emitir una nota de credito contra un comprobante previamente emitido.
6. **Punto de venta:** La informacion del punto de venta del emisor se incluye en el comprobante.
