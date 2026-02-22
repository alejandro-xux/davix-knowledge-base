# Flujo: Admision por Procedimiento

## Descripcion

Este flujo describe el proceso para registrar la admision de un paciente que sera atendido en un procedimiento medico (consulta, tomografia, rayos X, ecografia o procedimiento quirurgico).

## Actores involucrados

| Actor | Responsabilidad |
|-------|----------------|
| Admisionista | Registra la admision y agenda la cita |
| Paciente | Persona que sera atendida |
| Medico | Profesional que realizara la atencion |

## Precondiciones

- Debe existir una **venta activa** asociada al paciente
- El **medico** debe tener disponibilidad en su agenda
- La **especialidad** debe estar configurada en el sistema

## Pasos del flujo

### Paso 1: Seleccionar modalidad

1. El admisionista elige la modalidad de atencion:
   - **En consultorio** (presencial)
   - **Virtual** (telemedicina)

### Paso 2: Definir tipo de atencion

1. Se selecciona el tipo:
   - **Consulta** - Primera visita
   - **Reconsulta** - Visita de seguimiento
   - **Procedimiento medico** - Intervencion especifica

### Paso 3: Seleccionar especialidad y medico

1. Se elige la **especialidad medica** requerida
2. Se selecciona el **medico** tratante de esa especialidad
3. El sistema carga los cupos disponibles del medico

### Paso 4: Agendar fecha y hora

1. El sistema muestra un **calendario de 7 dias** con la disponibilidad del medico
2. Para cada dia se visualizan las franjas horarias con cupos libres
3. El admisionista selecciona dia y hora
4. **Restriccion:** No se puede agendar con menos de 20 minutos de anticipacion

### Paso 5: Completar datos de la admision

1. Se verifica que el paciente este correctamente asociado
2. Se ingresa el **motivo de consulta** (opcional)
3. Se selecciona el **lugar** de atencion

### Paso 6: Registrar datos especializados (segun tipo)

#### Para Tomografia:
- Tipo de estudio
- Region anatomica
- Uso de contraste
- Equipo medico

#### Para Rayos X:
- Tipo de proyeccion
- Region anatomica
- Equipo asignado

#### Para Ecografia:
- Tipo de ecografia
- Region anatomica

#### Para Procedimiento medico:
- Tipo de procedimiento
- Sala asignada
- Equipo requerido

### Paso 7: Confirmar admision

1. Se valida la informacion completa
2. La admision se crea en estado **EN ESPERA**
3. Se reserva el cupo en la agenda del medico

## Seguimiento de estados

```
EN ESPERA (0)
   ├─→ EN LLAMADO (1) ─→ EN ATENCION (2) ─→ ATENDIDO (3) ✓
   ├─→ REPROGRAMADO (5) ─→ EN ESPERA (nueva fecha)
   ├─→ BAJA (4)
   └─→ BAJA POR VENTA (6) [si se cancela la venta]
```

### Descripcion de cada estado

| Estado | Accion del sistema |
|--------|-------------------|
| En espera | Paciente aguarda en sala de espera |
| En llamado | Se llama al paciente para pasar a atencion |
| En atencion | El medico esta atendiendo al paciente |
| Atendido | La atencion fue completada exitosamente |
| Baja | Admision cancelada manualmente |
| Reprogramado | Se asigna nueva fecha; vuelve a "En espera" |
| Baja por venta | Cancelacion automatica al anular la venta |

## Postcondiciones

- La admision queda registrada con estado y seguimiento
- El cupo del medico queda reservado para la fecha seleccionada
- Al completar la atencion (ATENDIDO), se puede proceder al cobro

## Excepciones

| Excepcion | Accion |
|-----------|--------|
| Sin cupos disponibles | El admisionista debe buscar otra fecha u otro medico |
| Hora demasiado proxima | El sistema impide agendar con menos de 20 min de anticipacion |
| Venta cancelada | Todas las admisiones de esa venta pasan automaticamente a BAJA POR VENTA |
| Paciente no se presenta | El admisionista puede cambiar a BAJA o REPROGRAMADO |
