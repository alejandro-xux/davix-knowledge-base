# Admisiones

## Descripcion

El modulo de Admisiones gestiona el registro de pacientes que seran atendidos en procedimientos medicos. Soporta multiples tipos de procedimiento y lleva un seguimiento de estados desde la espera hasta la atencion completada.

## Tipos de admision

| Tipo | Descripcion |
|------|-------------|
| Consulta general | Admision para consulta medica estandar |
| Tomografia | Admision para estudios de tomografia |
| Rayos X | Admision para estudios radiograficos |
| Ecografia | Admision para estudios ecograficos |
| Procedimiento medico | Admision para procedimientos quirurgicos o especializados |

## Campos del formulario de admision

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Modalidad | Selector | Si | EN CONSULTORIO (1) o VIRTUAL (2) |
| Tipo de atencion | Selector | Si | CONSULTA, RECONSULTA o PROCEDIMIENTO MEDICO |
| Motivo de consulta | Texto | No | Razon de la visita del paciente |
| Especialidad | Selector | Si | Especialidad medica requerida |
| Medico | Selector | Si | Profesional que atendera |
| Paciente | Buscador | Si | Paciente a admitir |
| Fecha de atencion | Fecha/Hora | Si | Fecha y hora programada |
| Lugar | Selector | Si | Ubicacion del servicio |

## Agendamiento

El sistema genera un calendario de disponibilidad de 7 dias basado en:

- **Horarios del medico** - Configurados en el modulo de RRHH
- **Cupos disponibles** - Cantidad de citas por franja horaria
- **Duracion de atencion** - Por defecto 20 minutos
- **Anticipacion minima** - 20 minutos antes de la hora programada

### Estructura del calendario

Para cada dia de la semana se muestra:
- Dia de la semana y fecha
- Franjas horarias disponibles
- Cupos ocupados y disponibles por franja

## Estados de una admision

| Estado | Codigo | Descripcion |
|--------|--------|-------------|
| En espera | 0 | Paciente registrado, aguardando ser llamado |
| En llamado | 1 | Paciente esta siendo llamado |
| En atencion | 2 | Paciente esta siendo atendido |
| Atendido | 3 | Atencion completada exitosamente |
| Baja | 4 | Admision cancelada |
| Reprogramado | 5 | Cita reprogramada para otra fecha |
| Baja por venta | 6 | Cancelada por anulacion de la venta asociada |

### Diagrama de transiciones

```
EN ESPERA → EN LLAMADO → EN ATENCION → ATENDIDO
EN ESPERA → REPROGRAMADO → EN ESPERA (nueva fecha)
EN ESPERA → BAJA
EN ATENCION → BAJA
Cualquier estado → BAJA POR VENTA (si se cancela la venta)
```

## Admisiones especializadas

### Tomografia
Campos adicionales especificos para estudios tomograficos:
- Tipo de estudio
- Region anatomica
- Contraste (si/no)
- Equipo medico asignado

### Rayos X
Campos adicionales para estudios radiograficos:
- Tipo de proyeccion
- Region anatomica
- Equipo de rayos X

### Ecografia
Campos adicionales para estudios ecograficos:
- Tipo de ecografia
- Region anatomica

### Procedimiento medico
Campos adicionales para procedimientos:
- Tipo de procedimiento
- Sala asignada
- Equipo medico requerido

## Reglas de negocio

1. **Vinculacion con venta:** Toda admision debe estar asociada a una venta activa.
2. **Disponibilidad:** Solo se pueden crear admisiones en horarios con cupos disponibles.
3. **Anticipacion:** No se pueden agendar citas con menos de 20 minutos de anticipacion.
4. **Cancelacion en cascada:** Si una venta se da de baja, todas sus admisiones pasan a estado "Baja por venta" (codigo 6).
5. **Reprogramacion:** Un paciente reprogramado vuelve al estado "En espera" con nueva fecha.
