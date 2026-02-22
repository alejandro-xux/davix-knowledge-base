# Integraciones Externas

## SUNAT - Superintendencia Nacional de Aduanas y de Administracion Tributaria

### Consulta de RUC
- **Endpoint:** `api/v1/sunat/empresas`
- **Proposito:** Validar y obtener datos de empresas a partir de su numero de RUC
- **Uso en el sistema:** Al registrar un cliente empresa, se consulta SUNAT para autocompletar razon social, direccion y estado del contribuyente

### Emision de comprobantes electronicos
- **Proposito:** Envio de facturas, boletas y notas de credito a SUNAT
- **Tipos de documento soportados:**
  - Factura (codigo 01)
  - Boleta de venta (codigo 03)
  - Nota de credito (codigo 07)
  - Guia de remision (codigo 09)
- **Flag de control:** Campo `enviar_sunat` en el formulario de emision

## RENIEC - Registro Nacional de Identificacion y Estado Civil

### Consulta de DNI
- **Endpoint:** `api/v1/reniec/personas`
- **Proposito:** Validar y obtener datos de personas naturales a partir de su DNI
- **Uso en el sistema:** Al registrar un paciente o cliente persona, se consulta RENIEC para autocompletar nombres, apellidos y datos de identificacion
- **Datos obtenidos:** Apellido paterno, apellido materno, nombres, fecha de nacimiento

## Microservicios internos Davix

### Modulo de Salud
| Servicio | Datos consumidos |
|----------|-----------------|
| Pacientes | Datos demograficos, historial |
| Medicos | Profesionales, especialidades |
| Citas | Agenda, disponibilidad |
| Admisiones | Estado de admisiones |
| Convenios | Acuerdos con aseguradoras |
| Especialidades | Catalogo de especialidades medicas |
| Equipos medicos | Equipamiento disponible |

### Modulo de Logistica
| Servicio | Datos consumidos |
|----------|-----------------|
| Stocks | Disponibilidad de productos e insumos |
| Kardex | Trazabilidad de inventario |

### Modulo de RRHH
| Servicio | Datos consumidos |
|----------|-----------------|
| Colaboradores | Datos de vendedores y responsables |
| Horarios | Configuracion de turnos para agendamiento |

### Servicios transversales
| Servicio | Funcion |
|----------|---------|
| Parametros globales | Configuracion de series, impuestos, etc. |
| QR Codes | Generacion de codigos QR para comprobantes |
| Report Factory | Motor de generacion de reportes PDF |
| File Server | Almacenamiento y recuperacion de archivos |
