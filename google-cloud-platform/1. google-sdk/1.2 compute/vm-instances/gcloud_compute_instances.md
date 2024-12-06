
**Tags:** #gcp #compute #vm
**Description:** Manage virtual machine instances in Google Cloud with essential commands like `gcloud compute instances create` and `gcloud compute ssh`.
**Related to:** [[gcloud_compute_disks]]

## **VM Instance Management in Google Cloud**

### **List Existing Instances**

```bash
gcloud compute instances list
```

- Displays a list of all VM instances in your project.
- Includes details such as name, zone, status, machine type, and IP address.

### **Create a VM Instance**

```bash
gcloud compute instances create instance-name     --zone=zone-name     --machine-type=machine-type     --image-family=ubuntu-2004-lts     --image-project=ubuntu-os-cloud     --boot-disk-size=size-in-gb
```

- **`instance-name`:** Name of the instance.
- **`zone-name`:** Zone where the instance will be created (e.g., `us-central1-a`).
- **`machine-type`:** Machine type (e.g., `n1-standard-1`, `e2-medium`, etc.).
- **`image-family`:** Base image family (e.g., `ubuntu-2004-lts`).
- **`image-project`:** Base image project (e.g., `ubuntu-os-cloud` for Ubuntu images).
- **`boot-disk-size`:** Boot disk size in GB.

### **Connect to an Instance via SSH**

```bash
gcloud compute ssh instance-name     --zone=zone-name
```

- Opens an SSH connection to the specified instance.
- Automatically sets up the necessary SSH keys.

## **Additional Options:**

### **Use a Specific SSH Key:**

```bash
gcloud compute ssh instance-name     --zone=zone-name     --ssh-key-file=/path/to/key
```

### **Specify a User:**

```bash
gcloud compute ssh username@instance-name     --zone=zone-name
```

### **Stop an Instance**

```bash
gcloud compute instances stop instance-name     --zone=zone-name
```

- Stops an instance to save costs.
- Stopped instances still incur disk costs.

### **Start a Stopped Instance**

```bash
gcloud compute instances start instance-name     --zone=zone-name
```

- Starts a previously stopped instance.

### **Restart an Instance**

```bash
gcloud compute instances reset instance-name     --zone=zone-name
```

- Forces a restart of an instance.
- **Note:** This is similar to pressing the physical reset button on a machine.

### **Delete an Instance**

```bash
gcloud compute instances delete instance-name     --zone=zone-name
```

- Permanently deletes an instance.
- **Note:** Disks associated with the instance are also deleted unless specified otherwise.

### **Keep Disks When Deleting the Instance:**

```bash
gcloud compute instances delete instance-name     --zone=zone-name     --keep-disks=all
```

## **Disk Management for Instances**

### **Attach an Existing Disk**

```bash
gcloud compute instances attach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Attaches an existing disk to an instance.

### **Detach a Disk**

```bash
gcloud compute instances detach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Disconnects a disk from an instance.

## **Network and Firewall Configuration**

### **List Instance IP Addresses**

```bash
gcloud compute instances list     --format="table(name, networkInterfaces[0].accessConfigs[0].natIP)"
```

- Displays the external IP addresses of all instances.

### **Assign a Static IP**

```bash
gcloud compute addresses create static-ip-name     --region=region-name
```

- Reserves a static IP in the specified region.

```bash
gcloud compute instances network-interfaces update instance-name     --zone=zone-name     --addresses=static-ip-name
```

- Assigns the static IP to an instance.

## **Instance Disk Snapshots**

### **Create a Boot Disk Snapshot**

```bash
gcloud compute disks snapshot instance-name     --zone=zone-name     --snapshot-names=snapshot-name
```

- Creates a snapshot of an instance's boot disk.

### **Automate with Scripts**

Run a command on the instance:

```bash
gcloud compute ssh instance-name     --zone=zone-name     --command="command-to-run"
```

- Runs a specific command on an instance via SSH.

---

### **Related Links**

- [[gcloud_compute_disks]]: Commands to manage disks and images associated with instances.
- [[gcloud_iam_roles.md]]: Information on permissions required to work with VM instances.
- [[gcloud_networking.md]]: Advanced network and firewall configuration in GCP.

---

### **Notes**

- **Required Permissions:** Ensure you have permissions like `roles/compute.admin` or specific ones like `roles/compute.instanceAdmin`.
- **Cost Awareness:** Running instances incur continuous costs. Stop instances that you're not using.
- **Zones and Regions:** Create instances in zones close to your end users to minimize latency.
- **SSH Key Management:** Keys are automatically managed but can be customized as needed.
