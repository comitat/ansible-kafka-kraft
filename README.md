# Ansible Playbook for Deploying Kafka with Podman on CentOS

This Ansible playbook automates the deployment of Kafka using Podman on a CentOS system. It includes tasks for configuring the system, setting up disks, installing necessary packages, and configuring services.

## Features
- Disables SELinux for compatibility
- Configures systemd runtime directory
- Creates and mounts additional disks
- Installs Podman (version 5.3.2-2.el9)
- Sets up required directories for Kafka
- Creates and enables systemd service for Kafka

## Requirements
- Ansible installed on the control machine
- Target hosts running CentOS 9
- Additional disks available for Kafka storage (specified in `additional_disks` variable)

## Usage
1. Update the inventory file with target hosts.
2. Define required variables.
3. Run the playbook:

```sh
ansible-playbook -i inventory/inventory.yaml kafka-kraft.yaml
```

## Installation Process
### 1. System Preparation
- Retrieves user information
- Sets systemd runtime directory
- Disables SELinux for compatibility

### 2. Disk Partitioning & Mounting
- Checks available disks
- Creates partitions and formats them
- Retrieves UUIDs and mounts the partitions

### 3. Podman Installation & Kafka Setup
- Installs Podman version 5.3.2-2.el9
- Creates necessary directories for Kafka
- Configures systemd service for Kafka container
- Enables and starts the Kafka service

## Customization
Modify the `additional_disks` and `container_image_list` variables to match your environment requirements. Ensure that the correct image for Kafka is used in `container_image_list`.

## Troubleshooting
- Check system logs using:
  ```sh
  journalctl -u kafka.service -f
  ```
- Verify disk partitions and mount points:
  ```sh
  lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT
  ```
- Restart Kafka service if necessary:
  ```sh
  systemctl restart kafka.service
  ```

## License
MIT License

---
This README provides an overview of the Ansible playbook's functionality and usage. Adjust configurations as needed to fit your infrastructure.