Etiquetas: #gcp #compute #storage
Descripción: Comandos para manejar discos (`gcloud compute disks list`) e imágenes (`gcloud compute images create`).  
Relacionado con: [[gcloud_compute_instances]]

#### **Gestión de Discos en Google Cloud**

##### **Listar discos existentes**

```bash
gcloud compute disks list
```

- Muestra una lista de todos los discos disponibles en tu proyecto.
- Incluye detalles como el nombre, tamaño, tipo y la región donde se encuentran.

##### **Crear un disco**

```bash
gcloud compute disks create disk-name \
    --size=size-in-gb \
    --type=pd-standard \
    --zone=zone-name
```

- **`disk-name`:** Nombre del disco que deseas crear.
- **`size-in-gb`:** Tamaño del disco en GB (por ejemplo, 100 para un disco de 100 GB).
- **`pd-standard`:** Tipo de disco. Opciones comunes:
  - `pd-standard` (HDD estándar).
  - `pd-ssd` (SSD de alto rendimiento).
- **`zone-name`:** Zona donde se creará el disco (por ejemplo, `us-central1-a`).

##### **Eliminar un disco**

```bash
gcloud compute disks delete disk-name \
    --zone=zone-name
```

- Borra un disco especificado por su nombre y zona.

##### **Redimensionar un disco**

```bash
gcloud compute disks resize disk-name \
    --size=new-size-in-gb \
    --zone=zone-name
```

- Cambia el tamaño de un disco existente.
- **Nota:** Este cambio solo afecta al disco; también deberás extender el sistema de archivos en la instancia que lo use.

##### **Clonar un disco**

```bash
gcloud compute disks create new-disk-name \
    --source-disk=source-disk-name \
    --source-disk-zone=source-zone \
    --zone=destination-zone
```

- Crea un nuevo disco basado en uno existente.
- Útil para realizar copias o backups.

#### **Gestión de Imágenes en Google Cloud**

##### **Listar imágenes disponibles**

```bash
gcloud compute images list
```

Muestra todas las imágenes disponibles, tanto públicas como privadas (en tu proyecto).

##### **Crear una imagen desde un disco**

```bash
gcloud compute images create image-name \
    --source-disk=source-disk-name \
    --source-disk-zone=source-zone
```

- Crea una imagen basada en un disco existente.
- **`image-name`:** Nombre de la imagen que deseas crear.
- **`source-disk-name`:** Nombre del disco fuente.
- **`source-zone`:** Zona donde se encuentra el disco.

##### **Crear una imagen desde un archivo de disco (custom image)**

```bash
gcloud compute images create image-name \
    --source-uri=gs://bucket-name/path-to-image-file
```

- Crea una imagen personalizada desde un archivo almacenado en un bucket de Google Cloud Storage.

##### **Eliminar una imagen**

```bash
gcloud compute images delete image-name
```

- Borra una imagen especificada por su nombre.

##### **Exportar una imagen a un archivo**

```bash
gcloud compute images export \
    --destination-uri=gs://bucket-name/path-to-exported-image \
    --image=image-name
```

- Exporta una imagen a un archivo en Google Cloud Storage.
- **`destination-uri`:** Ruta en Cloud Storage donde se guardará el archivo.

#### **Adjuntar y Desadjuntar Discos**

##### **Adjuntar un disco a una instancia**

```bash
gcloud compute instances attach-disk instance-name \
    --disk=disk-name \
    --zone=zone-name
```

- Conecta un disco existente a una instancia.
- **Nota:** El disco debe estar en la misma zona que la instancia.

##### **Desadjuntar un disco de una instancia**

```bash
gcloud compute instances detach-disk instance-name \
    --disk=disk-name \
    --zone=zone-name
```

- Desconecta un disco de una instancia sin eliminarlo.

#### **Snapshot de Discos**

##### **Crear un snapshot**

```bash
gcloud compute disks snapshot disk-name \
    --snapshot-names=snapshot-name \
    --zone=zone-name
```

- Crea un snapshot (copia de seguridad) de un disco existente.

##### **Listar snapshots**

```bash
gcloud compute snapshots list
```

- Muestra una lista de todos los snapshots disponibles en tu proyecto.

##### **Eliminar un snapshot**

```bash
gcloud compute snapshots delete snapshot-name
```

- Borra un snapshot especificado por su nombre.

##### **Buenas Prácticas**

1. **Nombres descriptivos:** Usa nombres claros para discos e imágenes, como `web-server-disk` o `backup-image-2023-01`.
2. **Backups regulares:** Configura snapshots automáticos para discos críticos.
3. **Optimización de costos:** Revisa periódicamente discos y snapshots para eliminar recursos no utilizados.
4. **Zonas y regiones:** Asegúrate de crear discos y snapshots en regiones cercanas a tus usuarios o servicios.

---

##### **Enlaces Relacionados**

- [[gcloud_compute_instances]]: Comandos para gestionar instancias de máquinas virtuales en Google Cloud.
- [[gcloud_storage.md]]: Guía para trabajar con buckets y objetos en Cloud Storage.
- [[gcloud_iam_roles.md]]: Información sobre roles y permisos necesarios para administrar recursos en GCP.

---

##### **Notas**

- **Permisos necesarios:**
  - Para gestionar discos: asegúrate de tener permisos como `roles/compute.admin` o específicos como `roles/compute.storageAdmin`.
  - Para snapshots e imágenes: necesitarás permisos como `roles/compute.imageUser` o `roles/compute.snapshotUser`.

- **Cuidado con los costos:**
  - Discos no utilizados y snapshots antiguos pueden generar costos innecesarios. Configura políticas de limpieza o utiliza herramientas como "Recomendaciones de Google Cloud" para optimizar recursos.

- **Snapshots e imágenes en producción:**
  - Configura snapshots automáticos para discos críticos y almacena imágenes personalizadas para entornos reproducibles.

- **Zonas y regiones:**
  - Los discos, snapshots e imágenes deben estar en la misma región o zona que los recursos que los utilizarán para evitar latencias o errores de conexión.
