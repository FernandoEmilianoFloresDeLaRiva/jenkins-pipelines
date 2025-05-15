# Jenkins Pipeline

Este documento describe los **requisitos** y **secretos** necesarios para ejecutar correctamente todos pipeline definido en este repositorio.

---

## Variables y Secrets necesarios

El pipeline utiliza variables y secretos que **deben estar configurados en Jenkins** como "Credentials". La mayoría de los secretos varían por entorno (`production`, `qa`, `development`).

### 1. Clave SSH para despliegue

- **ID:** `ssh-key-ec2`
- **Tipo:** SSH Username with private key
- **Descripción:** Llave privada para acceso SSH al servidor de despliegue.

### 2. Variables de Base de Datos (por entorno)

Para cada entorno (`production`, `qa`, `development`), debes crear los siguientes secretos:

| Variable   | Tipo         | ID en Jenkins                | Notas                |
|------------|--------------|------------------------------|----------------------|
| DB_HOST    | Secret Text  | db-host-(entorno)            | Host de la base de datos |
| DB_USER    | Secret Text  | db-user-(entorno)            | Usuario de la base de datos |
| DB_PASS    | Secret Text  | db-pass-(entorno)           | Contraseña (secreta) |
| DB_NAME    | Secret Text  | db-name-(entorno)           | Nombre de la base de datos |

**Ejemplo de IDs:**

- `db-host-production`
- `db-user-qa`
- `db-pass-development`

### 3. Otras variables

- `EC2_USER`, `EC2_IP` y `REMOTE_PATH` están en el Jenkinsfile y no requieren secreto.
- `JWT_SECRET` está hardcodeado en el pipeline.
