# Configuracion

## Descripcion

El modulo de Configuracion gestiona los parametros del sistema, la validacion de procesos de venta, la exportacion de datos y el seguimiento de estados.

## Funcionalidades

### Configuracion de ventas
- Parametros generales del modulo de ventas
- Configuracion de series de documentos
- Asignacion de puntos de venta a vendedores

### Validacion de procesos
- Ejecucion de verificaciones automaticas sobre las ventas
- Deteccion de inconsistencias en datos
- Reporte de errores encontrados

### Exportacion a Excel
- Exportacion de listados y reportes en formato Excel
- Filtros aplicables antes de la exportacion

### Busqueda global
- Buscador transversal que permite encontrar ventas, pacientes, clientes y cobros
- Busqueda por nombre, documento o numero de comprobante

### Estados de ventas
- Panel de seguimiento de estados de todas las ventas
- Contadores por estado (Nuevo, Verificado, Cerrado, Baja)

## Parametros del sistema

Los parametros se obtienen del servicio global: `v2.0.1/erpx/global/params`

| Parametro | Descripcion |
|-----------|-------------|
| Series de boleta | Series habilitadas para emision de boletas |
| Series de factura | Series habilitadas para emision de facturas |
| Impuestos | Catalogo de impuestos aplicables (IGV, ISC) |
| Monedas | Monedas habilitadas (Soles, Dolares) |
| Tipos de documento | Tipos de documento de identidad |
| Puntos de venta | Ubicaciones fisicas de atencion |

## Configuracion de vendedores

Endpoint: `v2.0.1/erpx/comercial/configs-vendedores`

Permite asignar:
- Punto de venta por defecto para cada vendedor
- Permisos de operacion
- Series de comprobantes autorizadas

## Reglas de negocio

1. **Parametros centralizados:** Los parametros se gestionan desde el modulo Global y se consumen por todos los modulos.
2. **Verificacion obligatoria:** Antes de cerrar una venta, debe ejecutarse el proceso de validacion.
3. **Configuracion por punto de venta:** Las series y parametros pueden variar segun el punto de venta.
