# Sistema de Gestion Comercial

## Davix Healthcare Platform

El **Sistema de Gestion Comercial** es uno de los modulos principales de la plataforma Davix Healthcare. Se encarga de gestionar todo el ciclo comercial de los servicios de salud: desde la venta y facturacion hasta el cobro y la conciliacion de caja.

## Funcionalidades principales

| Modulo | Descripcion |
|--------|-------------|
| [Ventas](modulos/ventas.md) | Creacion, verificacion y cierre de ventas de servicios de salud |
| [Admisiones](modulos/admisiones.md) | Registro de admisiones para procedimientos medicos |
| [Cobros](modulos/cobros.md) | Gestion de cobranzas totales y parciales |
| [Cajas](modulos/cajas.md) | Apertura, movimientos y cierre de caja diaria |
| [Cierre](modulos/cierre.md) | Conciliacion financiera y resumen de movimientos |
| [Clientes](modulos/clientes.md) | Registro y gestion de clientes (personas y empresas) |
| [Pacientes](modulos/pacientes.md) | Registro y gestion de pacientes |
| [Medicos](modulos/medicos.md) | Gestion de profesionales de salud |
| [Comprobantes](modulos/comprobantes.md) | Emision de facturas, boletas, notas de credito y guias |
| [Configuracion](modulos/configuracion.md) | Parametros y validaciones del sistema |

## Flujos de negocio

- [Venta de servicio de salud](flujos/venta-servicio-salud.md)
- [Admision por procedimiento](flujos/admision-procedimiento.md)
- [Cobro de pagos](flujos/cobro-pagos.md)
- [Gestion de caja diaria](flujos/gestion-caja-diaria.md)

## Integraciones

El sistema se integra con:
- **SUNAT** - Consulta de RUC y emision de comprobantes electronicos
- **RENIEC** - Validacion de DNI de personas
- **Microservicios Davix** - Facturacion, finanzas, salud, logistica y RRHH
