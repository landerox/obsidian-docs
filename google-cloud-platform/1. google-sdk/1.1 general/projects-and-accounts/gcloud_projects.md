
Etiquetas: #gcp #projects
Descripción: Gestión de proyectos y cuentas en GCP (`gcloud projects list`, `gcloud organizations`).  
Relacionado con: [[gcloud_auth.md]], [[gcloud_billing.md]]

##### **Listar Proyectos**

Comando para ver todos los proyectos disponibles asociados con tu cuenta activa:

```bash
gcloud projects list
```

Este comando muestra una tabla con:

- **Project ID**: Identificador único del proyecto.
- **Name**: Nombre del proyecto.
- **Project Number**: Número único asignado por GCP.
- **Lifecycle State**: Estado actual del proyecto (e.g., ACTIVE).

##### **Crear un Proyecto Nuevo**

Puedes crear un proyecto utilizando el siguiente comando:

```bash
gcloud projects create [PROJECT_ID] --name="[PROJECT_NAME]"
```

- `[PROJECT_ID]`: Un identificador único para el proyecto (minúsculas, números y guiones).
- `[PROJECT_NAME]`: Nombre legible del proyecto.

Asociar el proyecto a una cuenta de facturación específica:

```bash
gcloud projects create [PROJECT_ID] --name="[PROJECT_NAME]" --billing-account="[BILLING_ACCOUNT_ID]"
```

##### **Cambiar el Proyecto Activo**

Para trabajar con un proyecto específico, debes configurarlo como activo:

```bash
gcloud config set project [PROJECT_ID]
```

Puedes verificar qué proyecto está activo actualmente:

```bash
gcloud config get-value project
```

##### **Borrar un Proyecto**

Para eliminar un proyecto (recuerda que los datos y recursos se perderán):

```bash
gcloud projects delete [PROJECT_ID]
```

##### **Ver Organizaciones**

Para listar todas las organizaciones asociadas a tu cuenta:

```bash
gcloud organizations list
```

##### **Mover un Proyecto a una Organización**

Si necesitas asignar un proyecto a una organización específica:

```bash
gcloud projects move [PROJECT_ID] --organization=[ORG_ID]
```

##### **Enlaces Relacionados**

- [[gcloud_auth.md]]: Aprende cómo autenticarte y configurar tu cuenta en GCP antes de gestionar proyectos.
- [[gcloud_billing.md]]: Configuración y gestión de cuentas de facturación asociadas a tus proyectos.

##### **Notas**

- **Permisos necesarios**: Asegúrate de tener los permisos adecuados para gestionar proyectos, como `roles/resourcemanager.projectCreator` o `roles/owner`.
- **Cuentas de facturación**: Todo proyecto debe estar asociado a una cuenta de facturación para habilitar recursos pagos.
