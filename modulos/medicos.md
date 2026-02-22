# Medicos

## Descripcion

El modulo de Medicos gestiona el registro de los profesionales de salud que brindan atencion en el centro. Incluye datos personales, especialidades, correos y telefonos de contacto.

## Campos del formulario

### Datos personales

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Nombres | Texto | Si | Nombres del profesional |
| Apellidos | Texto | Si | Apellidos del profesional |
| Tipo de documento | Selector | Si | DNI, Carnet de extranjeria, etc. |
| Numero de documento | Texto | Si | Numero de identificacion |
| Especialidad | Selector | Si | Especialidad medica principal |

### Informacion de contacto

#### Correo electronico
- Direccion de correo del profesional
- Puede tener multiples correos

#### Telefono
- Numero de contacto del profesional
- Puede tener multiples telefonos

## Entidades relacionadas

### Especialidades
- Catalogo de especialidades medicas disponibles
- Endpoint: `v2.0.2/erpx/salud/especialidades`
- Cada medico tiene al menos una especialidad

### Medicos referentes
- Medicos externos que refieren pacientes al centro
- Endpoint: `v2.0.3/erpx/salud/medicos-referentes`
- Se vinculan a las ventas como referentes

### Cupos (disponibilidad)
- Configuracion de horarios y cupos de atencion
- Franjas horarias con capacidad maxima de pacientes
- Se consulta al crear admisiones para verificar disponibilidad

## Relacion con otros modulos

| Modulo | Relacion |
|--------|----------|
| Ventas | Se registra como medico referente en la venta |
| Admisiones | Se selecciona como medico tratante |
| RRHH | Datos de horarios y turnos |

## Reglas de negocio

1. **Especialidad obligatoria:** Todo medico debe tener al menos una especialidad asignada.
2. **Cupos de atencion:** Los cupos definen la capacidad de agenda del medico por franja horaria.
3. **Medico referente vs tratante:** Un medico puede ser referente (externo que envia pacientes) o tratante (el que atiende en el centro).
4. **Validacion de documento:** El numero de documento se valida contra RENIEC si es DNI.
