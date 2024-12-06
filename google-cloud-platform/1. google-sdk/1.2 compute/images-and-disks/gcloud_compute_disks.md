**File:** [[gcloud_compute_disks.md]]
**Tags:** #gcp #compute #storage
**Description:** Commands to manage disks (`gcloud compute disks list`) and images (`gcloud compute images create`).
**Related to:** [[gcloud_compute_instances]]

## **Disk Management in Google Cloud**

### **List Existing Disks**

```bash
gcloud compute disks list
```

- Displays a list of all available disks in your project.
- Includes details such as the name, size, type, and the region where they are located.

### **Create a Disk**

```bash
gcloud compute disks create disk-name     --size=size-in-gb     --type=pd-standard     --zone=zone-name
```

- **`disk-name`:** Name of the disk you want to create.
- **`size-in-gb`:** Disk size in GB (e.g., 100 for a 100 GB disk).
- **`pd-standard`:** Disk type. Common options:
  - `pd-standard` (Standard HDD).
  - `pd-ssd` (High-performance SSD).
- **`zone-name`:** Zone where the disk will be created (e.g., `us-central1-a`).

### **Delete a Disk**

```bash
gcloud compute disks delete disk-name     --zone=zone-name
```

- Deletes a disk specified by its name and zone.

### **Resize a Disk**

```bash
gcloud compute disks resize disk-name     --size=new-size-in-gb     --zone=zone-name
```

- Changes the size of an existing disk.
- **Note:** This change only affects the disk; you must also extend the file system on the instance using it.

### **Clone a Disk**

```bash
gcloud compute disks create new-disk-name     --source-disk=source-disk-name     --source-disk-zone=source-zone     --zone=destination-zone
```

- Creates a new disk based on an existing one.
- Useful for making copies or backups.

## **Image Management in Google Cloud**

### **List Available Images**

```bash
gcloud compute images list
```

- Displays all available images, both public and private (in your project).

### **Create an Image from a Disk**

```bash
gcloud compute images create image-name     --source-disk=source-disk-name     --source-disk-zone=source-zone
```

- Creates an image based on an existing disk.
- **`image-name`:** Name of the image you want to create.
- **`source-disk-name`:** Name of the source disk.
- **`source-zone`:** Zone where the disk is located.

### **Create an Image from a Disk File (Custom Image)**

```bash
gcloud compute images create image-name     --source-uri=gs://bucket-name/path-to-image-file
```

- Creates a custom image from a file stored in a Google Cloud Storage bucket.

### **Delete an Image**

```bash
gcloud compute images delete image-name
```

- Deletes an image specified by its name.

### **Export an Image to a File**

```bash
gcloud compute images export     --destination-uri=gs://bucket-name/path-to-exported-image     --image=image-name
```

- Exports an image to a file in Google Cloud Storage.
- **`destination-uri`:** Path in Cloud Storage where the file will be saved.

## **Attach and Detach Disks**

### **Attach a Disk to an Instance**

```bash
gcloud compute instances attach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Connects an existing disk to an instance.
- **Note:** The disk must be in the same zone as the instance.

### **Detach a Disk from an Instance**

```bash
gcloud compute instances detach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Disconnects a disk from an instance without deleting it.

## **Disk Snapshots**

### **Create a Snapshot**

```bash
gcloud compute disks snapshot disk-name     --snapshot-names=snapshot-name     --zone=zone-name
```

- Creates a snapshot (backup) of an existing disk.

### **List Snapshots**

```bash
gcloud compute snapshots list
```

- Displays a list of all snapshots available in your project.

### **Delete a Snapshot**

```bash
gcloud compute snapshots delete snapshot-name
```

- Deletes a snapshot specified by its name.

### **Best Practices**

1. **Descriptive Names:** Use clear names for disks and images, like `web-server-disk` or `backup-image-2023-01`.
2. **Regular Backups:** Set up automatic snapshots for critical disks.
3. **Cost Optimization:** Periodically review disks and snapshots to remove unused resources.
4. **Zones and Regions:** Ensure disks and snapshots are created in regions close to your users or services.

---

### **Related Links**

- [[gcloud_compute_instances]]: Commands to manage virtual machine instances in Google Cloud.
- [[gcloud_storage.md]]: Guide for working with buckets and objects in Cloud Storage.
- [[gcloud_iam_roles.md]]: Information on roles and permissions required to manage resources in GCP.

---

### **Notes**

- **Required Permissions:**
  - To manage disks: ensure you have permissions like `roles/compute.admin` or specific ones like `roles/compute.storageAdmin`.
  - For snapshots and images: you need permissions like `roles/compute.imageUser` or `roles/compute.snapshotUser`.

- **Cost Awareness:**
  - Unused disks and old snapshots can incur unnecessary costs. Set up cleanup policies or use tools like "Google Cloud Recommendations" to optimize resources.

- **Snapshots and Images in Production:**
  - Configure automatic snapshots for critical disks and store custom images for reproducible environments.

- **Zones and Regions:**
  - Disks, snapshots, and images should be in the same region or zone as the resources using them to avoid latency or connection errors.
