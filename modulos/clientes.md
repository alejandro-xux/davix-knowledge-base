# Clientes

## Descripcion

El modulo de Clientes gestiona el registro y mantenimiento de los datos de clientes del sistema. Soporta dos tipos principales: personas naturales y empresas. Los clientes se vinculan a las ventas para efectos de facturacion.

## Tipos de cliente

| Tipo | Documento requerido | Descripcion |
|------|---------------------|-------------|
| Persona natural | DNI, Carnet de extranjeria, Pasaporte | Individuo, se emite Boleta |
| Empresa | RUC (11 digitos) | Persona juridica, se emite Factura |

## Campos del formulario - Cliente persona

### Datos de identificacion

| Campo | Tipo | Obligatorio | Validacion | Descripcion |
|-------|------|-------------|------------|-------------|
| Tipo de documento | Selector | No | - | DNI, Carnet de extranjeria, Pasaporte |
| Numero de documento | Texto | Si | min 8, max 8 caracteres (DNI) | Numero del documento de identidad |
| Apellido paterno | Texto | Si | required | Primer apellido |
| Apellido materno | Texto | Si | required | Segundo apellido |
| Nombres | Texto | Si | required | Nombres completos |
| Sexo | Selector | Si | required | Genero del cliente |
| Fecha de nacimiento | Fecha | No | - | Fecha de nacimiento |

### Datos de ubicacion

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Direccion | Texto | No | Direccion completa |
| Pais | Selector | No | Pais de residencia |
| Ubigeo | Selector jerarquico | No | Region > Provincia > Distrito |

### Datos comerciales

| Campo | Tipo | Obligatorio | Descripcion |
|-------|------|-------------|-------------|
| Razon social | Texto | No | Nombre legal (solo empresas) |
| Nombre comercial | Texto | No | Nombre de fantasia |
| Matriz | Selector | No | Tipo de ubicacion comercial |
| Consumidor | Selector | No | Segmento de consumidor |
| Canal | Selector | No | Canal de venta |
| Sub canal | Selector | No | Subdivision del canal |
| Canal de venta | Selector | No | Metodo de venta |

### Informacion de contacto

#### Correos electronicos
- Se pueden agregar multiples correos
- Cada correo tiene: direccion, tipo (principal, secundario)

#### Telefonos
- Se pueden agregar multiples telefonos
- Cada telefono tiene: numero, tipo (celular, fijo), indicativo

#### Contactos
- Personas de contacto asociadas al cliente
- Cada contacto tiene: nombre, cargo, telefono, correo

### Puntos de venta

- Ubicaciones donde el cliente opera
- Cada punto de venta tiene: nombre, direccion, ubigeo

## Validaciones especiales

| Validacion | Descripcion |
|------------|-------------|
| Cliente existente | Verifica que no se duplique un cliente con el mismo documento |
| Persona/Empresa | Valida la consistencia entre tipo de cliente y tipo de documento |
| Contactos validos | Asegura que los datos de contacto sean correctos |
| Consulta RENIEC | Para DNI, autocompleta datos desde RENIEC |
| Consulta SUNAT | Para RUC, autocompleta datos desde SUNAT |

## Responsive

El formulario se adapta al dispositivo:
- **Desktop:** Dialogo al 70% del ancho de pantalla
- **Mobile:** Dialogo al 95% del ancho de pantalla

## Reglas de negocio

1. **DNI = 8 digitos:** El documento DNI debe tener exactamente 8 caracteres.
2. **RUC = 11 digitos:** El documento RUC debe tener exactamente 11 caracteres.
3. **Auto-completado:** Al ingresar un DNI valido, se consulta RENIEC y se autocompletap nombres y apellidos. Para RUC, se consulta SUNAT.
4. **No duplicados:** El sistema impide registrar dos clientes con el mismo numero de documento.
5. **Vinculacion con ventas:** Un cliente se asocia a una venta para determinar a quien se emite el comprobante de pago.
