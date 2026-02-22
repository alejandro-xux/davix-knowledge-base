# Descripcion del Sistema

## Que es el Sistema de Gestion Comercial

El Sistema de Gestion Comercial es el modulo de la plataforma **Davix Healthcare** responsable de administrar el ciclo comercial completo de los servicios de salud. Abarca desde el registro de la venta hasta la emision del comprobante de pago y la conciliacion financiera diaria.

## Alcance funcional

El sistema cubre las siguientes areas:

### Gestion de ventas
- Registro de ventas de servicios y productos medicos
- Asociacion de pacientes y clientes a cada transaccion
- Seleccion de listas de precios y descuentos
- Validacion y verificacion de ventas antes del cierre
- Soporte para ventas al contado y a credito

### Gestion de admisiones
- Registro de admisiones para procedimientos medicos
- Soporte para multiples tipos: tomografia, rayos X, ecografia, procedimientos quirurgicos
- Seguimiento de estados desde la espera hasta la atencion
- Agendamiento con disponibilidad de medicos

### Gestion financiera
- Cobranzas totales y parciales
- Apertura y cierre de caja diaria
- Registro de movimientos de ingreso y salida
- Conciliacion financiera diaria

### Facturacion electronica
- Emision de facturas y boletas
- Emision de notas de credito
- Generacion de guias de remision
- Integracion con SUNAT para envio electronico

### Gestion de maestros
- Registro de pacientes con datos demograficos completos
- Registro de clientes (personas naturales y empresas)
- Gestion de medicos y especialidades
- Configuracion de puntos de venta

## Usuarios del sistema

| Rol | Funciones principales |
|-----|----------------------|
| Cajero/Vendedor | Registra ventas, emite comprobantes, gestiona caja |
| Admisionista | Registra admisiones de pacientes para procedimientos |
| Cobrador | Gestiona cobranzas y verifica pagos |
| Administrador | Configura parametros, consulta reportes de cierre |

## Contexto dentro de Davix

El Sistema de Gestion Comercial se conecta con otros modulos de la plataforma:

- **Salud** - Consume datos de pacientes, medicos, especialidades, convenios y citas
- **Facturacion** - Envia datos para la generacion de documentos electronicos
- **Finanzas** - Registra cobros, movimientos de caja y conciliaciones
- **Logistica** - Consulta stocks de productos e insumos medicos
- **RRHH** - Obtiene datos de colaboradores (vendedores, responsables)
