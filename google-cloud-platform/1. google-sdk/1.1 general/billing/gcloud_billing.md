
Etiquetas: #gcp #billing
Descripción: Configuración y gestión de cuentas de facturación (`gcloud billing accounts list`, `gcloud billing projects link`).
Relacionado con: [[gcloud_projects.md]], [[gcloud_auth.md]]

##### **Listar cuentas de facturación disponibles**

```bash
gcloud billing accounts list
```

Este comando muestra las cuentas de facturación disponibles asociadas con tu usuario o tu organización.

##### **Consultar la información de una cuenta de facturación específica**

```bash
gcloud billing accounts describe [ACCOUNT_ID]
```

Reemplaza `[ACCOUNT_ID]` con el identificador de la cuenta.

##### **Verificar si un proyecto tiene facturación habilitada**

```bash
gcloud beta billing projects describe [PROJECT_ID]
```

Reemplaza `[PROJECT_ID]` con el ID del proyecto.

##### **Vincular un proyecto a una cuenta de facturación**

Este comando habilita la facturación en un proyecto al vincularlo con una cuenta de facturación.

```bash
gcloud beta billing projects link [PROJECT_ID] --billing-account [ACCOUNT_ID]
```

##### **Deshabilitar la facturación de un proyecto**

Este comando deshabilita la facturación del proyecto.

```bash
gcloud beta billing projects unlink [PROJECT_ID]
```

**Nota:** Deshabilitar la facturación no elimina los recursos existentes, pero puede suspender servicios que dependan de ella.

##### **Crea una alerta de presupuesto con un límite definido:**

```bash
gcloud billing budgets create \
    --billing-account [ACCOUNT_ID] \
    --display-name "My Budget" \
    --amount 100.00 \
    --threshold-rules "0.5=EMAIL,1.0=EMAIL"
```

- **`--amount`**: Establece el límite de presupuesto (en dólares).
- **`--threshold-rules`**: Define umbrales para alertas; en este caso, el 50% y el 100%.

##### **Lista los presupuestos existentes:**

```bash
gcloud billing budgets list --billing-account [ACCOUNT_ID]
```

##### **Eliminar un presupuesto:**

```bash
gcloud billing budgets delete [BUDGET_NAME]
```

##### **Enlaces Relacionados**

- [[gcloud_auth.md]]: Aprende cómo autenticarse para gestionar cuentas de facturación.
- [[gcloud_projects.md]]: Cómo crear y gestionar proyectos antes de vincularlos a cuentas de facturación.
- [[gcloud_monitoring_alerts.md]]: Cómo configurar políticas de monitoreo y alertas relacionadas con costos.

##### **Notas**

- **Permisos necesarios**: Para gestionar cuentas de facturación, necesitas el rol `roles/billing.admin` o permisos específicos en la organización. Para vincular proyectos a cuentas de facturación, necesitas ser propietario o editor del proyecto.
- **Cuentas de facturación**: Configura cuentas de facturación antes de vincularlas a los proyectos para habilitar recursos pagos.
- **Límites de facturación**: Configura presupuestos y alertas de costos para evitar cargos inesperados utilizando los comandos de presupuestos.
- **Documentación oficial**: Consulta la documentación oficial de facturación de Google Cloud para obtener más detalles y casos avanzados.
