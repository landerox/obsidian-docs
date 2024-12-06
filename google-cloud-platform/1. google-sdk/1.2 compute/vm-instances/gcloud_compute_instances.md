**File:** [[gcloud_compute_disks.md]]
**Tags:** #gcp #compute #vm
**Description:** Manage virtual machine instances in Google Cloud with essential commands like `gcloud compute instances create` and `gcloud compute ssh`.
**Related to:** [[gcloud_compute_disks]]

#### **Gestión de Instancias de VM en Google Cloud**

##### **Listar instancias existentes**

```bash
gcloud compute instances list
```

- Muestra una lista de todas las instancias de VM en tu proyecto.
- Incluye detalles como el nombre, zona, estado, tipo de máquina y dirección IP.

##### **Crear una instancia de VM**

```bash
gcloud compute instances create instance-name \
    --zone=zone-name \
    --machine-type=machine-type \
    --image-family=ubuntu-2004-lts \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=size-in-gb
```

- **`instance-name`:** Nombre de la instancia.
- **`zone-name`:** Zona donde se creará la instancia (por ejemplo, `us-central1-a`).
- **`machine-type`:** Tipo de máquina (como `n1-standard-1`, `e2-medium`, etc.).
- **`image-family`:** Familia de imágenes base (por ejemplo, `ubuntu-2004-lts`).
- **`image-project`:** Proyecto de imagen base (como `ubuntu-os-cloud` para imágenes de Ubuntu).
- **`boot-disk-size`:** Tamaño del disco de arranque en GB.

##### **Conectarse a una instancia con SSH**

```bash
gcloud compute ssh instance-name \
    --zone=zone-name
```

- Abre una conexión SSH a la instancia especificada.
- Configura automáticamente las claves SSH necesarias.

###### **Opciones adicionales:**

###### **Usar una clave SSH específica:**

```bash
gcloud compute ssh instance-name \
    --zone=zone-name \
    --ssh-key-file=/path/to/key
```

###### **Especificar un usuario:**

```bash
gcloud compute ssh username@instance-name \
    --zone=zone-name
```

##### **Detener una instancia**

```bash
gcloud compute instances stop instance-name \
    --zone=zone-name
```

- Detiene una instancia para ahorrar costos.
- Las instancias detenidas siguen incurriendo en costos de disco.

##### **Iniciar una instancia detenida**

```bash
gcloud compute instances start instance-name \
    --zone=zone-name
Inicia una instancia previamente detenida.
```

##### **Reiniciar una instancia**

```bash
gcloud compute instances reset instance-name \
    --zone=zone-name
```

- Reinicia una instancia de manera forzada.
- **Nota:** Esta acción es similar a presionar el botón de reinicio físico en una máquina.

##### **Eliminar una instancia**

```bash
gcloud compute instances delete instance-name \
    --zone=zone-name
```

- Borra una instancia permanentemente.
- **Nota:** Los discos asociados a la instancia también se eliminan, a menos que se especifique lo contrario.

##### **Mantener discos al eliminar la instancia:**

```bash
gcloud compute instances delete instance-name \ --zone=zone-name \ --keep-disks=all
```

#### **Administración de Discos en Instancias**

##### **Adjuntar un disco existente**

```bash
gcloud compute instances attach-disk instance-name \
    --disk=disk-name \
    --zone=zone-name
```

- Adjunta un disco existente a una instancia.

##### **Desadjuntar un disco**

```bash
gcloud compute instances detach-disk instance-name \
    --disk=disk-name \
    --zone=zone-name
```

- Desconecta un disco de una instancia.

#### **Configuración de Red y Firewall**

##### **Listar direcciones IP de las instancias**

```bash
gcloud compute instances list \
    --format="table(name, networkInterfaces[0].accessConfigs[0].natIP)"
```

- Muestra las direcciones IP externas de todas las instancias.

##### **Asignar una IP estática**

```bash
gcloud compute addresses create static-ip-name \
    --region=region-name
```

Reserva una IP estática en la región especificada.

```bash
gcloud compute instances network-interfaces update instance-name \
    --zone=zone-name \
    --addresses=static-ip-name
```

- Asigna la IP estática a una instancia.

#### **Snapshots de Discos de Instancias**

##### **Crear un snapshot del disco de arranque**

```bash
gcloud compute disks snapshot instance-name \
    --zone=zone-name \
    --snapshot-names=snapshot-name
```

- Crea un snapshot del disco de arranque de una instancia.

##### **Automatización con Scripts**

Ejecutar un comando en la instancia

```bash
gcloud compute ssh instance-name \
    --zone=zone-name \
    --command="comando-a-ejecutar"
```

- Ejecuta un comando específico en una instancia vía SSH.

---

##### **Enlaces Relacionados**

- [[gcloud_compute_disks]]: Comandos para gestionar discos e imágenes asociados a instancias.
- [[gcloud_iam_roles.md]]: Información sobre permisos necesarios para trabajar con instancias de VM.
- [[gcloud_networking.md]]: Configuración avanzada de redes y firewalls en GCP.

---

##### **Notas**

- **Permisos necesarios:** Asegúrate de tener permisos como `roles/compute.admin` o específicos como `roles/compute.instanceAdmin`.
- **Cuidado con los costos:** Las instancias en ejecución generan costos continuos. Detén las que no estés utilizando.
- **Zonas y regiones:** Crea instancias en zonas cercanas a tus usuarios finales para minimizar la latencia.
- **Gestión de claves SSH:** Las claves se administran automáticamente, pero puedes personalizarlas según sea necesario.
