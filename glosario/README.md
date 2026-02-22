# Glosario

## Terminos del negocio

| Termino | Definicion |
|---------|-----------|
| **Admision** | Registro de ingreso de un paciente para ser atendido en un procedimiento o consulta medica |
| **Boleta** | Comprobante de pago electronico emitido a personas naturales (codigo SUNAT: 03) |
| **Caja diaria** | Registro financiero del flujo de efectivo de un cajero durante un turno o dia |
| **Cajero** | Usuario del sistema responsable de registrar ventas, emitir comprobantes y gestionar caja |
| **Cita** | Reserva de un horario con un medico para la atencion de un paciente |
| **Cobro** | Registro de un pago recibido contra una venta u operacion pendiente |
| **Cobro parcial** | Pago que cubre solo una parte del monto total adeudado |
| **Cobro total** | Pago que cubre la totalidad del monto adeudado en un solo acto |
| **Comprobante** | Documento tributario electronico (factura, boleta, nota de credito, guia de remision) |
| **Convenio** | Acuerdo entre el centro de salud y una aseguradora o institucion para la atencion de pacientes cubiertos |
| **Cupo** | Espacio disponible en la agenda de un medico para atender un paciente en una franja horaria |
| **Descuento global** | Rebaja aplicada al total de la venta, puede ser por porcentaje o monto fijo |
| **Factura** | Comprobante de pago electronico emitido a personas juridicas con RUC (codigo SUNAT: 01) |
| **Forma de pago** | Modalidad de pago: Contado (pago inmediato) o Credito (pago diferido en cuotas) |
| **Guia de remision** | Documento que sustenta el traslado de bienes (codigo SUNAT: 09) |
| **IGV** | Impuesto General a las Ventas. Impuesto al valor agregado aplicable en Peru (actualmente 18%) |
| **ISC** | Impuesto Selectivo al Consumo. Impuesto especifico a ciertos productos |
| **Lista de precios** | Catalogo con los precios de los servicios y productos disponibles para la venta |
| **Medico referente** | Profesional externo que refiere (envia) pacientes al centro de salud |
| **Medico tratante** | Profesional que atiende directamente al paciente en el centro de salud |
| **Nota de credito** | Documento que anula o modifica un comprobante emitido previamente (codigo SUNAT: 07) |
| **Operacion** | Transaccion comercial que puede ser una venta, cuenta o paquete |
| **Paquete** | Conjunto de servicios medicos agrupados bajo un precio especial |
| **Punto de venta** | Ubicacion fisica donde se realizan las ventas y se emiten comprobantes |
| **Serie** | Codigo alfanumerico que identifica el grupo de numeracion de un tipo de comprobante |
| **SOAT** | Seguro Obligatorio de Accidentes de Transito. Cobertura de emergencias por accidentes vehiculares |
| **Ubigeo** | Codigo de ubicacion geografica del Peru (Region > Provincia > Distrito) |
| **Vendedor** | Sinonimo de cajero en el contexto del sistema |
| **Verificacion** | Proceso de validacion que asegura la consistencia de los datos de una venta antes del cierre |
| **Vuelto** | Diferencia entre el efectivo recibido y el monto a cobrar, devuelta al cliente |

## Terminos tecnicos

| Termino | Definicion |
|---------|-----------|
| **DNI** | Documento Nacional de Identidad (Peru). 8 digitos. Emitido por RENIEC |
| **RENIEC** | Registro Nacional de Identificacion y Estado Civil. Entidad peruana que gestiona documentos de identidad |
| **RUC** | Registro Unico de Contribuyentes. 11 digitos. Identifica empresas y personas ante SUNAT |
| **SUNAT** | Superintendencia Nacional de Aduanas y de Administracion Tributaria. Autoridad tributaria de Peru |

## Estados

### Estados de venta

| Estado | Descripcion |
|--------|-------------|
| NUEVO | Venta recien creada, pendiente de procesamiento |
| SIN VERIFICAR | Venta que aun no ha pasado por el proceso de verificacion |
| VERIFICADO CON ERRORES | La verificacion detecto inconsistencias que deben corregirse |
| VERIFICADO CORRECTAMENTE | La verificacion fue exitosa, lista para cierre |
| CERRADO | Venta completada y finalizada |
| BAJA | Venta cancelada o anulada |

### Estados de admision

| Estado | Descripcion |
|--------|-------------|
| EN ESPERA | Paciente registrado, aguardando atencion |
| EN LLAMADO | Paciente esta siendo llamado |
| EN ATENCION | Paciente esta siendo atendido por el medico |
| ATENDIDO | Atencion completada exitosamente |
| BAJA | Admision cancelada |
| REPROGRAMADO | Cita movida a otra fecha |
| BAJA POR VENTA | Cancelada automaticamente al anular la venta |

### Estados de cita

| Estado | Descripcion |
|--------|-------------|
| NUEVO | Cita recien agendada |
| ATENDIDO | Paciente fue atendido |
| REPROGRAMADO | Cita movida a otra fecha |
| BAJA | Cita cancelada |
| BAJA POR VENTA | Cancelada al anular la venta |
