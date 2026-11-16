# Definition of Ready (DOR) - Solicitudes de ingesta

## Propósito

Una solicitud de tipo **Ingesta** está lista para construcción cuando contiene la información mínima necesaria para que el equipo de datos pueda implementar y certificar la solución sin depender de información esencial pendiente.

No se deben incluir contraseñas, tokens, claves API ni datos personales reales sin anonimizar.

## Campos obligatorios

### 1. Responsable de la fuente

Persona o equipo que administra la fuente de datos y puede resolver dudas sobre su disponibilidad, formato y contenido. Debe incluir nombre, área y medio de contacto.

### 2. Sistema de origen

Sistema, aplicación, plataforma o proveedor donde se generan originalmente los datos.

### 3. Nombre de la fuente de datos

Identificador específico de la fuente: archivo, tabla, API, endpoint o reporte.

### 4. Ubicación de la fuente

Ruta, URL, endpoint, bucket, esquema o ubicación técnica desde donde se obtendrán los datos. Las credenciales deben mantenerse en el gestor de credenciales.

### 5. Lógica de extracción

Descripción del método de extracción, filtros, parámetros, fecha de corte, campo incremental, tipo de carga —completa o incremental— y manejo de archivos procesados o fallidos.

### 6. Reglas de negocio

Reglas comprobables para validar, transformar, rechazar o aceptar los datos. Ejemplos: `customer_id` obligatorio, correo válido y ausencia de duplicados.

### 7. Responsable de datos

Persona responsable de aclarar el significado de los datos y validar funcionalmente el resultado. En este proyecto corresponde al rol **Data Research**.

### 8. Descripción de la solicitud

Objetivo de negocio, alcance y uso esperado de los datos.

### 9. Referencia de muestra de datos

Enlace, nombre de archivo o referencia a una muestra representativa. Debe estar anonimizada cuando contenga información sensible.

### 10. Volumetría esperada

Estimación de cantidad de registros, cantidad de archivos, tamaño aproximado y crecimiento esperado.

### 11. Frecuencia de carga

Periodicidad y horario de ejecución: frecuencia, días, hora y zona horaria.

## Criterio de cumplimiento

Una solicitud cumple el DOR cuando:

1. Los 11 campos están presentes.
2. Cada campo contiene información específica y no solo `pendiente`, `por definir` o `N/A`.
3. La lógica de extracción permite identificar el método de carga.
4. Las reglas de negocio son verificables.
5. Existe una muestra de datos o una justificación explícita de por qué no aplica.
6. La volumetría y frecuencia están informadas o cuentan con una estimación inicial validada.
7. No se exponen secretos ni datos sensibles sin anonimizar.

## Resultado esperado del agente validador

```json
{
  "cumple_dor": true,
  "porcentaje_completitud": 100,
  "campos_completos": [],
  "campos_faltantes": [],
  "observaciones": [],
  "accion_recomendada": "enviar_a_construccion"
}
```

Cuando falte información:

```json
{
  "cumple_dor": false,
  "porcentaje_completitud": 72,
  "campos_completos": [],
  "campos_faltantes": ["volumetria_esperada", "referencia_muestra_datos"],
  "observaciones": [
    "No se indicó el volumen estimado de registros.",
    "No se adjuntó una muestra anonimizada de los datos."
  ],
  "accion_recomendada": "solicitar_informacion"
}
```

## Acciones en Jira

| Resultado | Acción | Estado sugerido |
|---|---|---|
| Cumple el DOR | Agregar comentario y asignar al Data Engineer | `Listo Para Construcción` |
| No cumple el DOR | Agregar comentario con los campos faltantes | `Refinamiento` |
| Información completada | Ejecutar nuevamente la validación | `Refinamiento` |

## Plantilla de solicitud

```markdown
## Descripción de la solicitud

<!-- Objetivo, alcance y uso esperado -->

## Responsable de la fuente

- Nombre:
- Área:
- Correo o contacto:

## Sistema de origen

- Sistema o proveedor:

## Nombre de la fuente de datos

- Archivo, tabla, API o reporte:

## Ubicación de la fuente

- Ruta, URL, endpoint o referencia técnica:
- Tipo de conexión:

## Lógica de extracción

<!-- Método, filtros, incrementalidad, fecha de corte y manejo de errores -->

## Reglas de negocio

-

## Responsable de datos

- Nombre:
- Rol:
- Contacto:

## Referencia de muestra de datos

- Archivo o enlace:
- ¿Está anonimizada?:

## Volumetría esperada

- Registros:
- Tamaño:
- Crecimiento estimado:

## Frecuencia de carga

- Periodicidad:
- Hora:
- Días:
- Zona horaria:
```