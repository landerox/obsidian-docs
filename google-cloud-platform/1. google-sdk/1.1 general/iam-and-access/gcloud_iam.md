**Etiquetas:** #gcp #iam #roles
**Descripción:** Comandos para gestionar roles, permisos, y políticas de acceso (`gcloud iam roles`, `gcloud iam policy`).
Relacionado con: [[gcloud_projects.md]], [[gcloud_auth.md]]

##### **Listar roles disponibles**

```bash
gcloud iam roles list
```

Muestra todos los roles disponibles en tu proyecto u organización.

##### **Crear un rol personalizado**

```bash
gcloud iam roles create [ROLE_ID] \
    --project=[PROJECT_ID] \
    --title="Custom Role" \
    --description="Description of custom role" \
    --permissions="permission1,permission2" \
    --stage="GA"
```

[ROLE_ID]: Identificador único del rol.
[PROJECT_ID]: Proyecto donde se creará el rol.

##### **Actualizar un rol existente**

```bash
gcloud iam roles update [ROLE_ID] --project=[PROJECT_ID] --permissions="permission1,permission3"
```

##### **Eliminar un rol personalizado**

```bash
gcloud iam roles delete [ROLE_ID] --project=[PROJECT_ID]
```

##### **Asignar un rol a un usuario**

```bash
gcloud projects add-iam-policy-binding [PROJECT_ID] \
    --member="user:email@example.com" \
    --role="roles/[ROLE_NAME]"
```

##### **Revocar un rol de un usuario**

```bash
gcloud projects remove-iam-policy-binding [PROJECT_ID] \
    --member="user:email@example.com" \
    --role="roles/[ROLE_NAME]"
```

##### **Visualizar políticas IAM**

```bash
gcloud projects get-iam-policy [PROJECT_ID]
```

##### **Enlaces Relacionados**

- **[[gcloud_auth.md]]**: Aprende cómo autenticarse para acceder y gestionar políticas de IAM.
- **[[gcloud_projects.md]]**: Cómo gestionar proyectos, lo cual es esencial para asignar roles y permisos.
- **[[gcloud_iam_roles.md]]**: Información más detallada sobre roles predeterminados y personalizados en GCP.
- **[[gcloud_iam_policies.md]]**: Gestión avanzada de políticas de acceso y auditorías.
- **[[gcloud_monitoring_alerts.md]]**: Configuración de alertas para monitorear cambios en roles o políticas.

##### **Notas**

- **Permisos necesarios:** Requiere roles/owner o roles/iam.admin para ejecutar comandos avanzados de IAM.
- **Políticas organizacionales:** Configura políticas en niveles superiores como organizaciones o carpetas, si es necesario.
- **Documentación oficial:** Consulta la documentación oficial para roles específicos y casos avanzados.
