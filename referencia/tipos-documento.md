# Tipos de Documento

## Documentos de identidad

| Tipo | Codigo | Digitos | Validacion externa | Uso |
|------|--------|---------|-------------------|-----|
| DNI | 01 | 8 | RENIEC | Personas naturales peruanas |
| Carnet de extranjeria | 04 | Variable | - | Residentes extranjeros |
| Pasaporte | 07 | Variable | - | Ciudadanos extranjeros |
| Otro | 00 | Variable | - | Otros documentos |
| Sin documento | 00 | - | - | Emergencias |
| RUC | - | 11 | SUNAT | Empresas / personas juridicas |

### Reglas de validacion

- **DNI:** Exactamente 8 digitos numericos. Se valida contra RENIEC para obtener datos del titular.
- **RUC:** Exactamente 11 digitos numericos. Se valida contra SUNAT para obtener datos de la empresa.
- **Carnet de extranjeria y Pasaporte:** Longitud variable, sin validacion externa automatica.

---

## Comprobantes de pago (documentos tributarios)

| Tipo | Codigo SUNAT | Destinatario | Descripcion |
|------|-------------|--------------|-------------|
| Factura | 01 (interno: 1) | Empresas con RUC | Comprobante para personas juridicas |
| Boleta de venta | 03 (interno: 3) | Personas naturales | Comprobante para consumidores finales |
| Nota de credito | 07 (interno: 7) | Ambos | Anulacion o modificacion de comprobante emitido |
| Guia de remision | 09 (interno: 9) | Ambos | Sustento de traslado de bienes |

### Reglas de emision

| Regla | Descripcion |
|-------|-------------|
| Cliente empresa → Factura | Si el cliente tiene RUC, se debe emitir Factura |
| Cliente persona → Boleta | Si el cliente tiene DNI, se emite Boleta |
| Nota de credito | Solo se puede emitir contra un comprobante existente |
| Envio a SUNAT | Todos los comprobantes se envian electronicamente por defecto |

### Series

Cada tipo de comprobante tiene series configuradas:

| Parametro del sistema | Descripcion |
|-----------------------|-------------|
| SERIE-BOLETA | Series habilitadas para boletas (ej: B001, B002) |
| SERIE-FACTURA | Series habilitadas para facturas (ej: F001, F002) |

La numeracion dentro de cada serie es **correlativa y automatica**.

---

## Tipos de paciente

| Tipo | Descripcion | Impacto en facturacion |
|------|-------------|----------------------|
| PRIVADO | Paciente privado sin cobertura | Pago directo, comprobante a su nombre |
| PARTICULAR | Paciente particular | Pago directo |
| SOAT | Cubierto por SOAT | Facturacion a la aseguradora SOAT |
| CONVENIO | Cubierto por convenio | Facturacion al convenio/aseguradora |

---

## Tipos de operacion (cobros)

| Tipo | Descripcion |
|------|-------------|
| VENTA | Cobro asociado a una venta de servicio de salud |
| CUENTA | Cobro de una cuenta por cobrar |
| PAQUETE | Cobro de un paquete de servicios agrupados |

---

## Monedas

| Moneda | Codigo interno | Codigo ISO |
|--------|---------------|------------|
| Soles | 1 | PEN |
| Dolares | 2 | USD |
