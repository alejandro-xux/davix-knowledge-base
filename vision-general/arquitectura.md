# Arquitectura

## Stack tecnologico

| Componente | Tecnologia |
|-----------|-----------|
| Frontend | Angular |
| UI Components | PrimeNG (DataTable, Dialog, Dropdown, Calendar, etc.) |
| Formularios | Reactive Forms con validaciones dinamicas |
| Estado | RxJS Observables y Subjects |
| Precision numerica | BigNumber.js (2-3 decimales) |
| Visualizacion PDF | ng2-pdf-viewer |
| Estilos | Tailwind CSS + Design System propio |

## Arquitectura de microservicios

El frontend se comunica con un backend basado en microservicios a traves de una API REST.

**Servidor base:** `https://ms-pacs.davix.app`

### Dominios de API

| Dominio | Ruta base | Responsabilidad |
|---------|-----------|-----------------|
| Comercial | `/erpx/comercial/` | Ventas, clientes, catalogos, puntos de venta |
| Facturacion | `/erpx/facturacion/` | Documentos de venta (facturas, boletas, NC) |
| Finanzas | `/erpx/finanzas/` | Cobros, cajas diario, movimientos |
| Salud | `/erpx/salud/` | Pacientes, medicos, citas, admisiones, convenios |
| Logistica | `/erpx/logistica/` | Stocks, kardex |
| RRHH | `/erpx/rrhh/` | Colaboradores |
| Global | `/erpx/global/` | Parametros, QR codes |
| Reportes | `/erpx/reports/` | Generacion de reportes |
| Archivos | `/erpx/fserver/` | Gestion de archivos |

### Endpoints principales

#### Comercial
- `v2.0.6/erpx/comercial/ventas-salud` - CRUD de ventas
- `v2.0.4/erpx/comercial/gateway-ventas-salud` - Gateway de ventas
- `v2.0.3/erpx/comercial/clientes` - Gestion de clientes
- `v2.0.2/erpx/comercial/clientes-personas` - Clientes persona natural
- `v2.0.2/erpx/comercial/clientes-empresas` - Clientes empresa
- `v2.0.1/erpx/comercial/listas-precios` - Listas de precios
- `v2.0.1/erpx/comercial/puntos-ventas` - Puntos de venta
- `v2.0.1/erpx/comercial/configs-vendedores` - Configuracion de vendedores

#### Facturacion
- `v2.0.3/erpx/facturacion/documentos-ventas` - Documentos generales
- `v2.0.3/erpx/facturacion/documentos-ventas-facturas` - Facturas
- `v2.0.3/erpx/facturacion/documentos-ventas-boletas` - Boletas

#### Finanzas
- `v2.0.2/erpx/finanzas/cobros-ventas` - Cobros
- `v2.0.1/erpx/finanzas/cajas-diario` - Cajas diario
- `v2.0.1/erpx/finanzas/cajas-diario-movimientos` - Movimientos de caja
- `v2.0.1/erpx/finanzas/gateway-cobros-ventas` - Gateway de cobros

#### Salud
- `v2.0.3/erpx/salud/pacientes` - Pacientes
- `v2.0.4/erpx/salud/medicos` - Medicos
- `v2.0.2/erpx/salud/citas` - Citas
- `v2.0.3/erpx/salud/admisiones` - Admisiones
- `v2.0.1/erpx/salud/convenios` - Convenios
- `v2.0.2/erpx/salud/especialidades` - Especialidades

## Patron de comunicacion interna

El frontend utiliza un patron de comunicacion basado en **servicios reactivos**:

- **WebServiceVentasSaludService** - Servicio central de comunicacion HTTP (~1,025 lineas)
- **ComunicateServiceService** - Bus de eventos entre componentes via RxJS Subjects
- **ComunicateCobrosService** - Comunicacion especifica del modulo de cobros

### Flujo de datos tipico

```
Componente → ComunicateService (evento) → Componente destino
Componente → WebService (HTTP) → API REST → Microservicio
```

## Estructura de modulos Angular

```
mis-ventas-salud/
├── service/                    # Servicios centrales
├── models/                     # Enums y modelos
├── global/                     # Utilidades globales
├── list-ventas-salud/          # Listado de ventas
├── new-ventas-salud/           # Creacion de ventas
│   ├── new-admision/           # Admisiones
│   ├── new-cliente-persona/    # Registro de clientes
│   └── new-paciente/           # Registro de pacientes
├── list-mis-cobros/            # Gestion de cobros
├── list-mi-caja/               # Gestion de caja
├── list-resumen-cierre/        # Cierre y conciliacion
├── new-medico/                 # Registro de medicos
└── reports/                    # Comprobantes y reportes
```
