# Pacientes

## Descripcion

El modulo de Pacientes gestiona el registro de los pacientes que reciben servicios de salud. Almacena datos demograficos, documentos de identidad, informacion de contacto y la clasificacion por tipo de cobertura.

## Tipos de paciente

| Tipo | Descripcion |
|------|-------------|
| PRIVADO | Paciente atendido de forma privada, sin cobertura de seguro |
| PARTICULAR | Paciente particular con pago directo |
| SOAT | Paciente cubierto por Seguro Obligatorio de Accidentes de Transito |
| CONVENIO | Paciente cubierto por un convenio con aseguradora o institucion |

## Campos del formulario

### Datos de identificacion

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Tipo | Selector | No | PRIVADO, PARTICULAR, SOAT, CONVENIO (default: PRIVADO) |
| Tipo de documento | Selector | No | DNI, Carnet de extranjeria, Pasaporte, Otro, Sin documento |
| Numero de documento | Texto | No | Numero del documento de identidad |
| Apellido paterno | Texto | No | Primer apellido |
| Apellido materno | Texto | No | Segundo apellido |
| Nombres | Texto | No | Nombres completos |
| Sexo | Selector | No | Genero del paciente |
| Fecha de nacimiento | Fecha | No | Fecha de nacimiento |
| Edad | Numero | Auto | Calculada a partir de la fecha de nacimiento |
| Codigo | Texto | Auto | Codigo interno del paciente |

### Tipos de documento soportados

| Documento | Codigo tipo | Descripcion |
|-----------|-------------|-------------|
| DNI | 01 | Documento Nacional de Identidad (8 digitos) |
| Carnet de extranjeria | 04 | Para ciudadanos extranjeros residentes |
| Pasaporte | 07 | Documento internacional de viaje |
| Otro | 00 | Otro tipo de documento |
| Sin documento | 00 | Paciente sin documento (emergencias) |

### Datos de ubicacion

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Direccion | Texto | No | Direccion de domicilio |
| Pais | Selector | No | Pais de residencia |
| Ubigeo | Selector jerarquico | No | Region > Provincia > Distrito |

### Informacion de contacto

#### Correos electronicos
- Lista de correos asociados al paciente
- Campos: direccion de correo, tipo

#### Telefonos
- Lista de telefonos del paciente
- Campos: numero, tipo (celular, fijo), indicativo de pais

#### Contactos de emergencia
- Personas de contacto del paciente
- Campos: nombre, relacion, telefono, correo

## Estado de validacion

| Campo | Descripcion |
|-------|-------------|
| Estado de validacion | Indica si los datos del paciente fueron validados contra RENIEC |
| Fecha de validacion | Fecha en que se realizo la validacion |

## Componentes internos

El formulario de paciente se compone de subformularios independientes:

1. **PacienteUbigeosComponent** - Gestion de ubicacion geografica
2. **PacienteTelefonosComponent** - Gestion de numeros de telefono
3. **PacienteCorreosComponent** - Gestion de correos electronicos
4. **PacienteContactosComponent** - Gestion de contactos de emergencia

## Reglas de negocio

1. **Consulta RENIEC:** Al ingresar un DNI, el sistema consulta automaticamente RENIEC para obtener nombres y apellidos.
2. **Edad automatica:** La edad se calcula automaticamente a partir de la fecha de nacimiento.
3. **Sin documento:** Se permite registrar pacientes sin documento en casos de emergencia.
4. **Tipo define facturacion:** El tipo de paciente influye en como se factura el servicio (privado/particular vs. convenio/SOAT).
5. **Convenio asociado:** Si el tipo es CONVENIO, en la venta se debera seleccionar el convenio correspondiente.
6. **Fecha de registro:** Se asigna automaticamente la fecha actual al momento del registro.
