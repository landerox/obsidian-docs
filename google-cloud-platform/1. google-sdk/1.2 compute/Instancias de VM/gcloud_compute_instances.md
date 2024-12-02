
**Labels:** #gcp #compute #vm
**Description:** Management of virtual machine instances in Google Cloud with essential commands like `gcloud compute instances create` and `gcloud compute ssh`.  
**Related to:** [[gcloud_compute_disks.md]]

#### **VM Instance Management in Google Cloud**

##### **List existing instances**

```bash
gcloud compute instances list
```

- Displays a list of all VM instances in your project.
- Includes details such as name, zone, status, machine type, and IP address.

##### **Create a VM instance**

```bash
gcloud compute instances create instance-name     --zone=zone-name     --machine-type=machine-type     --image-family=ubuntu-2004-lts     --image-project=ubuntu-os-cloud     --boot-disk-size=size-in-gb
```

- **`instance-name`:** Name of the instance.
- **`zone-name`:** Zone where the instance will be created (e.g., `us-central1-a`).
- **`machine-type`:** Machine type (e.g., `n1-standard-1`, `e2-medium`, etc.).
- **`image-family`:** Base image family (e.g., `ubuntu-2004-lts`).
- **`image-project`:** Base image project (e.g., `ubuntu-os-cloud` for Ubuntu images).
- **`boot-disk-size`:** Boot disk size in GB.

##### **Connect to an instance via SSH**

```bash
gcloud compute ssh instance-name     --zone=zone-name
```

- Opens an SSH connection to the specified instance.
- Automatically configures the required SSH keys.

###### **Additional options:**

###### **Use a specific SSH key:**

```bash
gcloud compute ssh instance-name     --zone=zone-name     --ssh-key-file=/path/to/key
```

###### **Specify a user:**

```bash
gcloud compute ssh username@instance-name     --zone=zone-name
```

##### **Stop an instance**

```bash
gcloud compute instances stop instance-name     --zone=zone-name
```

- Stops an instance to save costs.
- Stopped instances still incur disk costs.

##### **Start a stopped instance**

```bash
gcloud compute instances start instance-name     --zone=zone-name
```

- Starts a previously stopped instance.

##### **Restart an instance**

```bash
gcloud compute instances reset instance-name     --zone=zone-name
```

- Forcefully restarts an instance.
- **Note:** This action is similar to pressing the physical reset button on a machine.

##### **Delete an instance**

```bash
gcloud compute instances delete instance-name     --zone=zone-name
```

- Permanently deletes an instance.
- **Note:** Associated disks are also deleted unless specified otherwise.

##### **Keep disks when deleting the instance:**

```bash
gcloud compute instances delete instance-name     --zone=zone-name     --keep-disks=all
```

#### **Disk Management for Instances**

##### **Attach an existing disk**

```bash
gcloud compute instances attach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Attaches an existing disk to an instance.

##### **Detach a disk**

```bash
gcloud compute instances detach-disk instance-name     --disk=disk-name     --zone=zone-name
```

- Disconnects a disk from an instance.

#### **Networking and Firewall Configuration**

##### **List IP addresses of instances**

```bash
gcloud compute instances list     --format="table(name, networkInterfaces[0].accessConfigs[0].natIP)"
```

- Displays the external IP addresses of all instances.

##### **Assign a static IP**

```bash
gcloud compute addresses create static-ip-name     --region=region-name
```

- Reserves a static IP in the specified region.

```bash
gcloud compute instances network-interfaces update instance-name     --zone=zone-name     --addresses=static-ip-name
```

- Assigns the static IP to an instance.

#### **Snapshots of Instance Disks**

##### **Create a snapshot of the boot disk**

```bash
gcloud compute disks snapshot instance-name     --zone=zone-name     --snapshot-names=snapshot-name
```

- Creates a snapshot of an instance's boot disk.

##### **Automation with Scripts**

Execute a command on the instance:

```bash
gcloud compute ssh instance-name     --zone=zone-name     --command="command-to-execute"
```

- Executes a specific command on an instance via SSH.

---

##### **Related Links**

- [[gcloud_compute_disks.md]]: Commands to manage disks and images associated with instances.
- [[gcloud_iam_roles.md]]: Information on permissions needed to work with VM instances.
- [[gcloud_networking.md]]: Advanced networking and firewall configuration in GCP.

---

##### **Notes**

- **Required permissions:** Ensure you have permissions like `roles/compute.admin` or specific ones like `roles/compute.instanceAdmin`.
- **Cost considerations:** Running instances incur ongoing costs. Stop unused instances to save money.
- **Zones and regions:** Create instances in zones close to your end users to minimize latency.
- **SSH key management:** Keys are managed automatically but can be customized as needed.
