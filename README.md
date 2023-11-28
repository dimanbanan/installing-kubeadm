# Installing kubeadm cluster using terrafrom and ansible on Yandex Cloud

### This project provides an automated way to deploy a Kubernetes cluster on Yandex Cloud using Terraform and Ansible tools.

------

### Features

- Deploying a Kubernetes cluster using Kubeadm.
- Yandex Cloud Cloud provider support.
- Using Terraform to manage the infrastructure and create the necessary resources.
- Ansible for configuring and installing Kubernetes on created virtual machines.

------

### Requirements

- A Yandex Cloud account with a configured project.
- Installed Terraform and Ansible tools on your local computer.

------

### Using

1. Configure Variables

In the notes directory, you need to create a terraform.auto.tfvars file, in which you need to specify the OAuth token, cloud_id, folder_id:

```
token = ""
cloud_id = ""
folder_id = ""
```

2. Run Terraform

```
cd nodes
terraform init
terraform apply
```

Terraform will create virtual machines, a hosts.txt file with machine addresses, and execute playbook.yml and master-forward.yml to configure the nodes

3. Connect to the master node, run the [flannel.sh](https://github.com/dimanbanan/installing-kubeadm/blob/edit-readme/files/flannel.sh) script to configure network interfaces. After that, copy the contents of the init.output.txt file and paste it into the join.yml file on the host machine. Execute [join.yml](https://github.com/dimanbanan/installing-kubeadm/blob/edit-readme/join.yml).

```
ansible-playbook -i inventory/hosts.txt join.yml

```

This playbook will connect worker nodes to the cluster.

------

### Notes

- Be sure to delete the created resources when they are no longer needed to avoid unnecessary expenses.
