# Estados y Transiciones

## Venta

### Estados

| Codigo | Estado | Color visual | Descripcion |
|--------|--------|-------------|-------------|
| 0 | NUEVO | Azul (info) | Venta recien creada |
| 1 | VERIFICADO CON ERRORES | Rojo (error) | Verificacion detecto problemas |
| 2 | VERIFICADO CORRECTAMENTE | Amarillo (warning) | Verificacion exitosa |
| 3 | CERRADO | Verde (success) | Venta finalizada |
| 4 | BAJA | Rojo (error) | Venta cancelada |
| 5 | SIN VERIFICAR | Gris (neutral) | No se ha verificado |

### Transiciones permitidas

```
NUEVO ──────────→ SIN VERIFICAR
   │                    │
   └──→ VERIFICADO CON ERRORES ──→ VERIFICADO CORRECTAMENTE ──→ CERRADO
                                          │
                                          └──→ (corregir) ──→ VERIFICADO CON ERRORES

Cualquier estado ──→ BAJA
```

---

## Admision

### Estados

| Codigo | Estado | Descripcion |
|--------|--------|-------------|
| 0 | EN ESPERA | Paciente aguarda ser llamado |
| 1 | EN LLAMADO | Paciente esta siendo llamado |
| 2 | EN ATENCION | Paciente en atencion activa |
| 3 | ATENDIDO | Atencion completada |
| 4 | BAJA | Admision cancelada |
| 5 | REPROGRAMADO | Cita reprogramada |
| 6 | BAJA POR VENTA | Cancelada por anulacion de venta |

### Transiciones permitidas

```
EN ESPERA ──→ EN LLAMADO ──→ EN ATENCION ──→ ATENDIDO ✓

EN ESPERA ──→ REPROGRAMADO ──→ EN ESPERA (nueva fecha)

EN ESPERA ──→ BAJA
EN ATENCION ──→ BAJA

Cualquier estado ──→ BAJA POR VENTA (automatico al anular venta)
```

---

## Cita

### Estados

| Codigo | Estado | Descripcion |
|--------|--------|-------------|
| 0 | NUEVO | Cita agendada |
| 1 | ATENDIDO | Paciente fue atendido |
| 2 | REPROGRAMADO | Cita movida a otra fecha |
| 3 | BAJA | Cita cancelada |
| 6 | BAJA POR VENTA | Cancelada por anulacion de venta |

### Transiciones permitidas

```
NUEVO ──→ ATENDIDO ✓
NUEVO ──→ REPROGRAMADO ──→ NUEVO (nueva fecha)
NUEVO ──→ BAJA
Cualquier estado ──→ BAJA POR VENTA
```

---

## Caja Diaria

### Estados

| Codigo | Estado | Descripcion |
|--------|--------|-------------|
| 0 | NUEVA (pendiente apertura) | Caja creada pero no abierta |
| 1 | ABIERTA (necesita cierre) | Caja operativa, recibe movimientos |
| 2 | CERRADA | Caja cerrada y conciliada |

### Transiciones

```
NUEVA (0) ──→ ABIERTA (1) ──→ CERRADA (2)
```

No hay retroceso: una caja cerrada no puede reabrirse.
