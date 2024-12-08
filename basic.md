# Sección 1: Guía Básica para Usar la API de Facturación de Latinium con Postman

## Requisitos Previos
- Postman, Insomnia o cualquier otro tipo de aplicacion que permita consimur API's instalado en tu computadora
- Credenciales proporcionadas por Elixir Software (username, password, tenantId) para el uso de la API

## Paso 1: Generar Token JWT
### Configuración de la Solicitud
- Abre Postman
- Crea una nueva solicitud POST
- URL: `https://sync.elixirsa.net:97/api/{tenantId}/Auth/login`
- URL Ejemplo: `https://sync.elixirsa.net:97/api/1/Auth/login`
- Método: POST

### Imagen 1: Configuración de Solicitud de Token
![Captura de pantalla de Postman mostrando](img/image1.png)
- Barra de URL con la dirección completa
- Método POST seleccionado
- Pestaña de Body seleccionada

### Body de la Solicitud
- Selecciona la pestaña "raw"
- Elige formato JSON
- Introduce el siguiente JSON:
```json
{
  "Username": "tu_usuario",
  "Password": "tu_contraseña"
}
```

### Imagen 2: Body de Solicitud de Token
![Captura de pantalla mostrando](img/image2a.png)
- Pestaña "raw" seleccionada
- Formato JSON
- JSON de login completado

## Paso 2: Crear una Factura
### Configuración de la Solicitud
- Crea una nueva solicitud POST
- URL: `https://sync.elixirsa.net:97/api/{tenantId}/Facturacion`
- URL Ejemplo: `https://sync.elixirsa.net:97/api/1/Facturacion`
- Método: POST

### Configuración de Headers
- Agrega un header:
  - Clave: `Authorization`
  - Valor: `Bearer {token_generado_en_paso_1}`

### Imagen 3: Headers para Solicitud de Factura
![Captura de pantalla mostrando](img/image3a.png)
- Pestaña de Headers
- Header de Authorization con token

### Body de la Solicitud de Factura
- Selecciona "raw" y JSON
- Usa el ejemplo de solicitud completa del documento

### Imagen 4: Body de Solicitud de Factura
![Captura de pantalla mostrando](img/image4a.png)
- Pestaña "raw" seleccionada
- Formato JSON
- JSON de facturación completado

## Consejos Importantes
- Reemplaza los valores de ejemplo con tus datos reales
- Verifica que todos los campos obligatorios estén completos
- Presta atención a los códigos de error

## Posibles Errores Comunes
- Credenciales incorrectas
- Campos obligatorios faltantes
- Tipos de datos incorrectos

## Validaciones Clave
- RUC debe tener 13 dígitos
- Cédula debe tener 10 dígitos
- Asegúrate de tener todos los códigos correctos (proyecto, subproyecto, etc.)

## Ejemplo Cuerpo Mínimo Funcional
```json
{
  "cliente": {
    "ruc": "1715282248",
    "nombre": "MONICA MOSCOSO",
    "direccion": "TADAY Y CAHUASQUI",
    "email": "erikportilla.pesantez@outlook.es",
    "telefono": "0968176565",
    "IdTipoRuc": 5
  },
  "compra": {
    "fechaEmision": "2024-11-22",
    "idTipoFactura": 1,
    "DiasCredito": 10,
    "Numero": "001001005298"
  },
  "detalles": [
    {
      "articulo": {
        "codigo": "API-ART-7",
        "nombre": "NUEVO PRODUCTO 2"
      },
      "cantidad": 4,
      "precio": 12,
      "descuento": 2,
      "impuesto": 15,
      "CodigoIva": "0"
    },
    {
      "articulo": {
        "codigo": "API-ART-2",
        "nombre": "NUEVO PRODUCTO 1"
      },
      "cantidad": 10,
      "precio": 15,
      "CodigoIva": "4"
    }
  ]
}
```

### Imagen 5: Respuesta Exitosa
![Captura de pantalla mostrando](/img/image5.png)
- Código de respuesta 200
- JSON de respuesta con `success: true`
- Número de factura generado

### Imagen 6: Respuesta Errónea
![Captura de pantalla mostrando](/img/image6.png)
- Código de respuesta 400
- JSON de respuesta con `success: false`
- Mensaje de error generado

## Recomendaciones Finales
- Prueba primero con datos de ejemplo en una base de datos de ejemplo
- Contacta con soporte de Elixir Software para dudas específicas
- Mantén tus credenciales seguras

[Seccion como usar con datos de ejemplo]: #

# Sección 2: Consumo de la API con Datos de Ejemplo

A continuación, se explica cómo consumir la API de Facturación de **Latinium** utilizando los siguientes datos de ejemplo:

- **TenantId**: `2`
- **Usuario**: `ElixirSoftware`
- **Contraseña**: `Elixir2024_`

Esta sección incluye pasos para generar un token JWT y crear una factura con datos de ejemplo.

## Paso 1: Generar el Token JWT

### Configuración de la Solicitud en Postman
1. Abre Postman y crea una nueva solicitud **POST**.
2. Configura la URL como:  
   `https://sync.elixirsa.net:97/api/2/Auth/login`  
   (Usa el **TenantId** `2` en la URL).

3. Selecciona la pestaña **Body** y elige la opción **raw** con formato **JSON**.  
   Introduce el siguiente cuerpo de la solicitud:
   ```json
   {
       "Username": "ElixirSoftware",
       "Password": "Elixir2024_"
   }
   ```

### Imagen: Solicitud para Generar el Token
![Configuración en Postman para la generación del token](img/image7.png)

### Respuesta Esperada
Al enviar la solicitud, recibirás una respuesta con un token JWT. El token se verá de la siguiente manera:
```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Copia el valor del campo `token`, ya que será necesario para los pasos siguientes.

---

## Paso 2: Crear una Factura con Datos de Ejemplo

### Configuración de la Solicitud
1. Crea una nueva solicitud **POST** en Postman.
2. Configura la URL como:  
   `https://sync.elixirsa.net:97/api/2/Facturacion`  
   (Usa el mismo **TenantId** `2`).

3. En la pestaña **Headers**, añade un encabezado con:
  - **Clave**: `Authorization`
  - **Valor**: `Bearer {token}` (reemplaza `{token}` con el valor obtenido en el Paso 1).

4. Selecciona la pestaña **Body**, elige **raw** y formato **JSON**. Introduce el siguiente JSON:
```json
{
  "cliente": {
    "ruc": "1715282248",
    "nombre": "MONICA MOSCOSO",
    "direccion": "TADAY Y CAHUASQUI",
    "email": "erikportilla.pesantez@outlook.es",
    "telefono": "0968176565",
    "IdTipoRuc": 5
  },
  "compra": {
    "fechaEmision": "2024-11-22",
    "idTipoFactura": 1,
    "DiasCredito": 10,
    "Numero": "001001005298"
  },
  "detalles": [
    {
      "articulo": {
        "codigo": "API-ART-7",
        "nombre": "NUEVO PRODUCTO 2"
      },
      "cantidad": 4,
      "precio": 12,
      "descuento": 2,
      "impuesto": 15,
      "CodigoIva": "0"
    },
    {
      "articulo": {
        "codigo": "API-ART-2",
        "nombre": "NUEVO PRODUCTO 1"
      },
      "cantidad": 10,
      "precio": 15,
      "CodigoIva": "4"
    }
  ]
}
```

### Imagen: Solicitud para Crear Factura

![Configuración en Postman para crear una factura](img/image9.png)
![Configuración en Postman para crear una factura](img/image8.png)

---

### Respuesta Esperada
Si los datos son válidos, recibirás una respuesta como esta:
```json
{
  "success": true,
  "message": "Se guardó la factura con Id: '001001005298' correctamente",
  "data": "001001005298",
  "time": 6477
}
```

### Imagen: Respuesta Exitosa
![Captura de pantalla mostrando](/img/image5.png)

---

## Resumen
Con estos datos de ejemplo, cualquier usuario puede probar la API de **Latinium**.  
**Importante**: Recuerda que estos datos son de prueba y no reflejan información real. Para el uso en producción, utiliza tus credenciales y datos específicos.