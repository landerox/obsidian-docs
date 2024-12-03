
File: [[gcloud_auth.md]]
Etiquetas: #gcp #auth #config
Descripción: Comandos para autenticarse en GCP y configurar tu CLI (`gcloud auth`, `gcloud config`).  
Relacionado con: [[gcloud_projects.md]], [[gcloud_billing.md]]

###### **Iniciar sesión con tu cuenta de Google**

```bash
gcloud auth login
```

- Abre una ventana del navegador para autenticarte.
- Útil para interactuar con GCP desde la CLI.

###### **Listar cuentas autenticadas**

```bash
gcloud auth list
```

- Muestra las cuentas autenticadas en tu sistema.
- Resalta cuál es la cuenta activa.

###### **Establecer una cuenta activa**

```bash
gcloud config set account user@google.com
```

Cambia la cuenta activa utilizada por los comandos de `gcloud`.

###### **Autenticación predeterminada para aplicaciones**

```bash
gcloud auth application-default login
```

- Se utiliza para autenticar aplicaciones que usan bibliotecas cliente de GCP.
- Genera credenciales en `~/.config/gcloud/application_default_credentials.json`.

**Nota**: Este método es útil principalmente para entornos de desarrollo. En producción, se recomienda usar credenciales de cuentas de servicio.

###### **Establecer credenciales para aplicaciones**

Linux/MacOS:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="~/.config/gcloud/application_default_credentials.json"

```

Windows (CMD):

```bash
set export GOOGLE_APPLICATION_CREDENTIALS="C:\Users\TuUsuario\.config\gcloud\application_default_credentials.json"
```

Windows (PowerShell):

```bash
$env:GOOGLE_APPLICATION_CREDENTIALS="C:\Users\TuUsuario\.config\gcloud\application_default_credentials.json"
```

##### **Revocar autenticación**

Para cuentas de usuario:

```bash
gcloud auth revoke user@google.com
```

Revoca el acceso de una cuenta específica.

Revocar todas las cuentas:

```bash
gcloud auth revoke --all
```

###### **Obtener un token de acceso manualmente**

```bash
gcloud auth print-access-token
```

- Genera un token que puedes usar para realizar solicitudes API directamente.
- Útil para pruebas rápidas o depuración.

###### **Configuración de perfiles con `gcloud`**

Crear una nueva configuración:

```bash
gcloud config configurations create new-config
```

###### **Cambiar entre configuraciones:**

```bash
gcloud config configurations activate config-name
```

###### **Listar configuraciones existentes:**

```bash
gcloud config configurations list
```

###### **Eliminar una configuración:**

```bash
gcloud config configurations delete config-name
```

##### **Enlaces Relacionados**

- [[gcloud_projects.md]]: Aprende cómo gestionar proyectos y cuentas en GCP.
- [[gcloud_billing.md]]: Configuración y gestión de cuentas de facturación asociadas a tus proyectos.
- [[gcloud_iam_roles.md]]: Información sobre roles y permisos en GCP.

---

##### **Notas**

- **Permisos necesarios:** Asegúrate de tener los permisos adecuados para ejecutar comandos de autenticación y configuración, como `roles/iam.serviceAccountUser` o `roles/owner`.
- **Cuentas de facturación:** Las credenciales de autenticación son necesarias para trabajar con recursos pagos asociados a cuentas de facturación.
- **Tokens de acceso:** Los tokens generados manualmente con `gcloud auth print-access-token` tienen una duración limitada (generalmente 1 hora) y no deben ser usados en producción.
