# Plan de Backups Del Sistema de Gestión Escolar

## 1. Objetivo

Establecer un procedimiento para realizar respaldos de la información del sistema, con el propósito de prevenir la pérdida de datos y permitir la recuperación de la información ante fallos, errores o eliminación accidental.

## 2. Información que será respaldada

Los respaldos estarán enfocados principalmente en la base de datos PostgreSQL utilizada por el sistema.

Se respaldará:

- La estructura de la base de datos.
- Los registros de la tabla `usuarios`.
- Los registros de la tabla `alumnos`.
- Las relaciones y restricciones definidas en la base de datos.

Las contraseñas de los usuarios no se almacenan en texto plano, sino mediante hashes seguros.

## 3. Frecuencia de los respaldos

| Tipo de respaldo | Frecuencia |
|---|---|
| Respaldo de la base de datos | Diario |
| Respaldo antes de cambios importantes | Cuando sea necesario |
| Verificación de respaldos | Semanal |

Se recomienda conservar respaldos de diferentes fechas para disponer de puntos de recuperación históricos.

## 4. Lugar de almacenamiento

Los respaldos deberán almacenarse en un medio independiente del servidor donde funciona la aplicación.

Se recomienda utilizar almacenamiento externo o en la nube, como:

- Google Drive.
- OneDrive.
- Amazon S3.
- Otro servicio de almacenamiento seguro.

Los archivos de respaldo deberán mantenerse protegidos mediante controles de acceso adecuados y no deberán publicarse ni almacenarse en repositorios públicos.

### Organización de los respaldos

```text
Backups/
├── 2026/
│   ├── 08/
│   │   ├── backup_2026-08-09.sql
│   │   ├── backup_2026-08-10.sql
│   │   └── backup_2026-08-11.sql
```

## 5. Procedimiento de recuperación ante fallos

En caso de pérdida, corrupción o eliminación accidental de información, se seguirá el siguiente procedimiento.

### Paso 1. Identificar el fallo

Determinar el origen del problema, por ejemplo:

- Pérdida de registros.
- Corrupción de la base de datos.
- Eliminación accidental de información.
- Error durante una actualización.
- Fallo del servicio de base de datos.

### Paso 2. Seleccionar el respaldo

Seleccionar el respaldo más reciente disponible que sea anterior al momento en que ocurrió el fallo.

### Paso 3. Preparar la base de datos

Verificar que la base de datos PostgreSQL esté disponible y que exista una conexión correcta con la aplicación.

### Paso 4. Restaurar el respaldo

Utilizar el archivo de respaldo para recuperar la estructura y los registros de la base de datos.

Por ejemplo:

```bash
psql -U usuario -d colegio_san_marcos -f backup.sql
```

Los parámetros deberán adaptarse a la configuración utilizada por el entorno de producción.

### Paso 5. Verificar la información

Después de realizar la restauración se deberá comprobar que:

- Las tablas existan correctamente.
- Los registros de usuarios estén disponibles.
- Los registros de alumnos estén disponibles.
- Las relaciones y restricciones funcionen correctamente.
- Los usuarios puedan iniciar sesión.
- La gestión de usuarios funcione.
- La gestión de alumnos funcione.

### Paso 6. Verificar la aplicación

Finalmente se realizarán pruebas de funcionamiento:

```text
Login
  ↓
Autenticación
  ↓
Gestión de usuarios
  ↓
Gestión de alumnos
  ↓
Base de datos PostgreSQL
```

Si las operaciones principales funcionan correctamente, se considerará completado el proceso de recuperación.

## 6. Verificación de los respaldos

Se realizará una verificación periódica para comprobar que:

- El archivo de respaldo exista.
- El archivo pueda ser leído.
- El respaldo corresponda a la fecha esperada.
- La información pueda ser restaurada correctamente.

Se recomienda realizar una prueba de restauración al menos una vez al mes.

## 7. Seguridad de los respaldos

Los archivos de respaldo deberán mantenerse protegidos debido a que pueden contener información de los usuarios y alumnos.

Se deberán aplicar las siguientes medidas:

- Restringir el acceso a los archivos.
- No almacenar respaldos en repositorios públicos.
- No compartir los archivos de respaldo públicamente.
- Utilizar almacenamiento seguro.
- Proteger las credenciales utilizadas para acceder a los respaldos.

## 8. Responsabilidad

La persona responsable de la administración del sistema deberá:

- Verificar que los respaldos se realicen de acuerdo con la frecuencia establecida.
- Comprobar periódicamente la disponibilidad de los respaldos.
- Mantener los respaldos organizados por fecha.
- Proteger los archivos contra accesos no autorizados.
- Realizar pruebas periódicas de recuperación.
- Ejecutar el procedimiento de restauración cuando sea necesario.

## 9. Resultado esperado

La implementación de este plan permitirá contar con copias de seguridad de la información del sistema y con un procedimiento definido para recuperar los datos ante fallos.

De esta manera se busca reducir el riesgo de pérdida de información y mantener la disponibilidad de la aplicación y de sus datos.

## 10. Autor
William Alexander Flores Cardona
Docente
