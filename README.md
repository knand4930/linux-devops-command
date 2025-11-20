# Complete DevOps Commands Reference Guide

A comprehensive guide covering all essential commands for DevOps engineers including Linux, Docker, Kubernetes, Git, CI/CD, and Cloud platforms.

## Table of Contents

- [Linux System Administration](#linux-system-administration)
- [Git & Version Control](#git--version-control)
- [Docker Commands](#docker-commands)
- [Kubernetes Commands](#kubernetes-commands)
- [CI/CD Tools](#cicd-tools)
- [AWS CLI Commands](#aws-cli-commands)
- [Azure CLI Commands](#azure-cli-commands)
- [GCP Commands](#gcp-commands)
- [Terraform Commands](#terraform-commands)
- [Ansible Commands](#ansible-commands)
- [Monitoring & Logging](#monitoring--logging)
- [Networking Commands](#networking-commands)
- [Package Management](#package-management)

---

## Linux System Administration

### File and Directory Operations

```bash
# List files
ls -la
ll

# Change directory
cd /path/to/directory
cd ~  # Home directory
cd -  # Previous directory

# Create directory
mkdir directory_name
mkdir -p path/to/nested/directory

# Remove files/directories
rm file.txt
rm -rf directory/

# Copy files
cp source.txt destination.txt
cp -r source_dir/ dest_dir/

# Move/rename
mv old_name new_name
mv file.txt /path/to/destination/

# View file contents
cat file.txt
less file.txt
head -n 10 file.txt
tail -f /var/log/syslog  # Follow log files

# Search in files
grep "pattern" file.txt
grep -r "pattern" directory/
grep -i "pattern" file.txt  # Case insensitive
```

### File Permissions

```bash
# Change permissions
chmod 755 script.sh
chmod +x script.sh
chmod u+x,g+r,o-w file.txt

# Change ownership
chown user:group file.txt
chown -R user:group directory/

# View permissions
ls -l file.txt
stat file.txt
```

### Process Management

```bash
# List processes
ps aux
ps -ef
ps aux | grep process_name

# Top processes
top
htop

# Kill process
kill PID
kill -9 PID  # Force kill
killall process_name
pkill -f pattern

# Background processes
command &
nohup command &
jobs
fg
bg

# Process priority
nice -n 10 command
renice -n 5 -p PID
```

### System Information

```bash
# System info
uname -a
hostnamectl
uptime
date

# CPU info
lscpu
cat /proc/cpuinfo

# Memory info
free -h
cat /proc/meminfo
vmstat

# Disk usage
df -h
du -sh directory/
du -h --max-depth=1

# Hardware info
lshw
lspci
lsusb
lsblk
```

### User Management

```bash
# Add user
useradd username
useradd -m -s /bin/bash username

# Modify user
usermod -aG sudo username
usermod -aG docker username

# Delete user
userdel username
userdel -r username  # Remove home directory

# Password management
passwd username
passwd -l username  # Lock account
passwd -u username  # Unlock account

# List users
cat /etc/passwd
who
w
id username
```

### Service Management (systemd)

```bash
# Service status
systemctl status service_name
systemctl is-active service_name
systemctl is-enabled service_name

# Start/Stop services
systemctl start service_name
systemctl stop service_name
systemctl restart service_name
systemctl reload service_name

# Enable/Disable services
systemctl enable service_name
systemctl disable service_name

# List services
systemctl list-units --type=service
systemctl list-units --type=service --state=running
systemctl list-unit-files

# View logs
journalctl -u service_name
journalctl -u service_name -f  # Follow
journalctl -u service_name --since today
```

### Networking

```bash
# Network interfaces
ip addr show
ip link show
ifconfig

# Routing
ip route show
route -n
traceroute google.com
mtr google.com

# DNS
nslookup domain.com
dig domain.com
host domain.com

# Network connections
netstat -tuln
netstat -anp
ss -tuln
ss -s

# Firewall (UFW)
ufw status
ufw enable
ufw allow 80/tcp
ufw allow from 192.168.1.0/24
ufw deny 22/tcp
ufw delete allow 80/tcp

# Firewall (firewalld)
firewall-cmd --state
firewall-cmd --list-all
firewall-cmd --add-port=8080/tcp --permanent
firewall-cmd --reload

# iptables
iptables -L -n -v
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables-save > /etc/iptables/rules.v4

# Test connectivity
ping -c 4 google.com
telnet host port
nc -zv host port
curl -I https://example.com
wget https://example.com/file
```

### Archive and Compression

```bash
# tar
tar -czf archive.tar.gz directory/
tar -xzf archive.tar.gz
tar -tzf archive.tar.gz  # List contents

# zip
zip -r archive.zip directory/
unzip archive.zip
unzip -l archive.zip  # List contents

# gzip
gzip file.txt
gunzip file.txt.gz

# bzip2
bzip2 file.txt
bunzip2 file.txt.bz2
```

---

## Git & Version Control

### Basic Git Commands

```bash
# Initialize repository
git init
git clone https://github.com/user/repo.git
git clone --branch branch_name https://github.com/user/repo.git

# Configuration
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git config --list

# Status and information
git status
git log
git log --oneline
git log --graph --oneline --all
git diff
git diff --staged

# Staging and commits
git add file.txt
git add .
git add -A
git commit -m "Commit message"
git commit -am "Add and commit"

# Branching
git branch
git branch branch_name
git checkout branch_name
git checkout -b new_branch
git switch branch_name
git branch -d branch_name
git branch -D branch_name  # Force delete

# Merging
git merge branch_name
git merge --no-ff branch_name
git rebase branch_name

# Remote operations
git remote -v
git remote add origin url
git push origin branch_name
git push -u origin branch_name
git pull origin branch_name
git fetch origin

# Undo changes
git reset HEAD file.txt
git reset --soft HEAD~1
git reset --hard HEAD~1
git revert commit_hash
git checkout -- file.txt

# Stashing
git stash
git stash list
git stash apply
git stash pop
git stash drop

# Tags
git tag
git tag v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin v1.0.0
git push origin --tags

# Advanced
git cherry-pick commit_hash
git reflog
git clean -fd
git blame file.txt
```

### Git Workflow Commands

```bash
# Feature branch workflow
git checkout -b feature/new-feature
git add .
git commit -m "Add new feature"
git push origin feature/new-feature

# Gitflow
git flow init
git flow feature start feature_name
git flow feature finish feature_name
git flow release start 1.0.0
git flow release finish 1.0.0

# Squash commits
git rebase -i HEAD~3

# Update forked repository
git remote add upstream original_repo_url
git fetch upstream
git merge upstream/main
```

---

## Docker Commands

### Container Management

```bash
# List containers
docker ps
docker ps -a
docker ps -aq  # Only IDs

# Run container
docker run image_name
docker run -d image_name  # Detached mode
docker run -it image_name /bin/bash  # Interactive
docker run -p 8080:80 image_name  # Port mapping
docker run -v /host/path:/container/path image_name  # Volume
docker run --name container_name image_name
docker run -e ENV_VAR=value image_name  # Environment variable
docker run --rm image_name  # Remove after exit

# Container operations
docker start container_id
docker stop container_id
docker restart container_id
docker pause container_id
docker unpause container_id
docker kill container_id

# Remove containers
docker rm container_id
docker rm -f container_id  # Force remove
docker container prune  # Remove all stopped

# Container inspection
docker logs container_id
docker logs -f container_id  # Follow
docker logs --tail 100 container_id
docker inspect container_id
docker stats
docker stats container_id
docker top container_id

# Execute commands in container
docker exec -it container_id /bin/bash
docker exec container_id command
docker attach container_id

# Copy files
docker cp container_id:/path/file.txt ./local/
docker cp ./local/file.txt container_id:/path/
```

### Image Management

```bash
# List images
docker images
docker images -a
docker image ls

# Pull/Push images
docker pull image_name:tag
docker push image_name:tag

# Build image
docker build -t image_name:tag .
docker build -t image_name:tag -f Dockerfile.dev .
docker build --no-cache -t image_name:tag .

# Remove images
docker rmi image_id
docker rmi -f image_id
docker image prune  # Remove unused
docker image prune -a  # Remove all unused

# Image inspection
docker history image_name
docker inspect image_name

# Tag image
docker tag source_image:tag target_image:tag

# Save/Load images
docker save -o image.tar image_name
docker load -i image.tar

# Export/Import containers
docker export container_id > container.tar
docker import container.tar image_name:tag
```

### Docker Compose

```bash
# Start services
docker-compose up
docker-compose up -d  # Detached mode
docker-compose up --build  # Rebuild images

# Stop services
docker-compose down
docker-compose down -v  # Remove volumes
docker-compose stop
docker-compose start

# View logs
docker-compose logs
docker-compose logs -f service_name
docker-compose logs --tail=100 service_name

# List services
docker-compose ps
docker-compose top

# Execute commands
docker-compose exec service_name command
docker-compose exec service_name /bin/bash

# Build images
docker-compose build
docker-compose build --no-cache

# Scale services
docker-compose up -d --scale service_name=3

# Restart services
docker-compose restart service_name
```

### Docker Network

```bash
# List networks
docker network ls

# Create network
docker network create network_name
docker network create --driver bridge network_name

# Inspect network
docker network inspect network_name

# Connect/Disconnect
docker network connect network_name container_id
docker network disconnect network_name container_id

# Remove network
docker network rm network_name
docker network prune
```

### Docker Volume

```bash
# List volumes
docker volume ls

# Create volume
docker volume create volume_name

# Inspect volume
docker volume inspect volume_name

# Remove volume
docker volume rm volume_name
docker volume prune
```

### Docker System

```bash
# System info
docker info
docker version

# Disk usage
docker system df

# Clean up
docker system prune
docker system prune -a
docker system prune -a --volumes
```

---

## Kubernetes Commands

### Cluster Information

```bash
# Cluster info
kubectl cluster-info
kubectl version
kubectl get nodes
kubectl describe node node_name
kubectl top nodes

# Context and config
kubectl config view
kubectl config get-contexts
kubectl config current-context
kubectl config use-context context_name
kubectl config set-context --current --namespace=namespace_name
```

### Pod Management

```bash
# List pods
kubectl get pods
kubectl get pods -A  # All namespaces
kubectl get pods -n namespace_name
kubectl get pods -o wide
kubectl get pods --watch

# Describe pod
kubectl describe pod pod_name
kubectl describe pod pod_name -n namespace_name

# Create pod
kubectl run pod_name --image=image_name
kubectl apply -f pod.yaml

# Delete pod
kubectl delete pod pod_name
kubectl delete pod pod_name --grace-period=0 --force

# Pod logs
kubectl logs pod_name
kubectl logs pod_name -c container_name
kubectl logs pod_name -f  # Follow
kubectl logs pod_name --previous  # Previous instance
kubectl logs -l app=myapp  # By label

# Execute commands in pod
kubectl exec -it pod_name -- /bin/bash
kubectl exec pod_name -- command
kubectl exec -it pod_name -c container_name -- /bin/bash

# Port forwarding
kubectl port-forward pod_name 8080:80
kubectl port-forward service/service_name 8080:80

# Copy files
kubectl cp pod_name:/path/file.txt ./local/
kubectl cp ./local/file.txt pod_name:/path/
```

### Deployment Management

```bash
# List deployments
kubectl get deployments
kubectl get deploy -A

# Create deployment
kubectl create deployment deployment_name --image=image_name
kubectl apply -f deployment.yaml

# Describe deployment
kubectl describe deployment deployment_name

# Scale deployment
kubectl scale deployment deployment_name --replicas=3
kubectl autoscale deployment deployment_name --min=2 --max=10 --cpu-percent=80

# Update deployment
kubectl set image deployment/deployment_name container_name=new_image:tag
kubectl rollout restart deployment deployment_name

# Rollout management
kubectl rollout status deployment deployment_name
kubectl rollout history deployment deployment_name
kubectl rollout undo deployment deployment_name
kubectl rollout undo deployment deployment_name --to-revision=2

# Delete deployment
kubectl delete deployment deployment_name
```

### Service Management

```bash
# List services
kubectl get services
kubectl get svc

# Create service
kubectl expose deployment deployment_name --port=80 --target-port=8080
kubectl apply -f service.yaml

# Describe service
kubectl describe service service_name

# Delete service
kubectl delete service service_name

# Service types
kubectl expose deployment deployment_name --type=NodePort --port=80
kubectl expose deployment deployment_name --type=LoadBalancer --port=80
```

### ConfigMap and Secrets

```bash
# ConfigMaps
kubectl get configmaps
kubectl create configmap config_name --from-file=config.conf
kubectl create configmap config_name --from-literal=key=value
kubectl describe configmap config_name
kubectl delete configmap config_name

# Secrets
kubectl get secrets
kubectl create secret generic secret_name --from-literal=password=secret123
kubectl create secret generic secret_name --from-file=ssh-key=~/.ssh/id_rsa
kubectl create secret docker-registry regcred --docker-server=server --docker-username=user --docker-password=pass
kubectl describe secret secret_name
kubectl delete secret secret_name
```

### Namespace Management

```bash
# List namespaces
kubectl get namespaces
kubectl get ns

# Create namespace
kubectl create namespace namespace_name

# Delete namespace
kubectl delete namespace namespace_name

# Set default namespace
kubectl config set-context --current --namespace=namespace_name
```

### Resource Management

```bash
# Get all resources
kubectl get all
kubectl get all -A

# Apply/Delete resources
kubectl apply -f file.yaml
kubectl apply -f directory/
kubectl apply -f https://url/to/file.yaml
kubectl delete -f file.yaml

# Edit resources
kubectl edit deployment deployment_name
kubectl edit service service_name

# Patch resources
kubectl patch deployment deployment_name -p '{"spec":{"replicas":3}}'

# Label resources
kubectl label pods pod_name env=production
kubectl label pods pod_name env-  # Remove label
```

### Ingress

```bash
# List ingress
kubectl get ingress
kubectl get ing -A

# Describe ingress
kubectl describe ingress ingress_name

# Create/Delete ingress
kubectl apply -f ingress.yaml
kubectl delete ingress ingress_name
```

### StatefulSet

```bash
# List StatefulSets
kubectl get statefulsets
kubectl get sts

# Describe StatefulSet
kubectl describe statefulset statefulset_name

# Scale StatefulSet
kubectl scale statefulset statefulset_name --replicas=3
```

### DaemonSet

```bash
# List DaemonSets
kubectl get daemonsets
kubectl get ds

# Describe DaemonSet
kubectl describe daemonset daemonset_name
```

### Jobs and CronJobs

```bash
# Jobs
kubectl get jobs
kubectl create job job_name --image=image_name -- command
kubectl describe job job_name
kubectl delete job job_name

# CronJobs
kubectl get cronjobs
kubectl get cj
kubectl create cronjob cronjob_name --image=image_name --schedule="*/5 * * * *" -- command
kubectl describe cronjob cronjob_name
```

### Persistent Volumes

```bash
# Persistent Volumes
kubectl get pv
kubectl describe pv pv_name

# Persistent Volume Claims
kubectl get pvc
kubectl describe pvc pvc_name
```

### Troubleshooting

```bash
# Events
kubectl get events
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get events -n namespace_name

# Resource usage
kubectl top nodes
kubectl top pods
kubectl top pods -A

# Debug
kubectl debug pod_name -it --image=busybox
kubectl run debug --rm -it --image=busybox -- /bin/sh

# Drain node
kubectl drain node_name --ignore-daemonsets
kubectl cordon node_name
kubectl uncordon node_name
```

### Helm Commands

```bash
# Repository management
helm repo add repo_name https://charts.example.com
helm repo update
helm repo list
helm repo remove repo_name

# Search charts
helm search repo chart_name
helm search hub chart_name

# Install chart
helm install release_name chart_name
helm install release_name chart_name --namespace namespace_name
helm install release_name chart_name --values values.yaml
helm install release_name chart_name --set key=value

# List releases
helm list
helm list -A

# Upgrade release
helm upgrade release_name chart_name
helm upgrade release_name chart_name --values values.yaml

# Rollback release
helm rollback release_name
helm rollback release_name revision_number

# Uninstall release
helm uninstall release_name

# History
helm history release_name

# Get values
helm get values release_name
helm get manifest release_name
```

---

## CI/CD Tools

### Jenkins CLI

```bash
# Build job
java -jar jenkins-cli.jar -s http://jenkins-server build job_name

# Get job info
java -jar jenkins-cli.jar -s http://jenkins-server get-job job_name

# Create job
java -jar jenkins-cli.jar -s http://jenkins-server create-job job_name < config.xml

# Delete job
java -jar jenkins-cli.jar -s http://jenkins-server delete-job job_name

# List jobs
java -jar jenkins-cli.jar -s http://jenkins-server list-jobs
```

### GitLab CI

```bash
# GitLab Runner
gitlab-runner register
gitlab-runner list
gitlab-runner verify
gitlab-runner start
gitlab-runner stop
gitlab-runner restart

# Pipeline
gitlab-runner exec docker job_name
```

### CircleCI CLI

```bash
# Validate config
circleci config validate

# Execute locally
circleci local execute

# Follow build
circleci follow username/project

# Open in browser
circleci open
```

---

## AWS CLI Commands

### EC2

```bash
# List instances
aws ec2 describe-instances
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table

# Start/Stop instances
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0

# Create instance
aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name mykey

# Security groups
aws ec2 describe-security-groups
aws ec2 create-security-group --group-name mysg --description "My security group"
aws ec2 authorize-security-group-ingress --group-id sg-12345678 --protocol tcp --port 22 --cidr 0.0.0.0/0

# Key pairs
aws ec2 describe-key-pairs
aws ec2 create-key-pair --key-name mykey --query 'KeyMaterial' --output text > mykey.pem

# AMIs
aws ec2 describe-images --owners self
aws ec2 create-image --instance-id i-1234567890abcdef0 --name "My AMI"
```

### S3

```bash
# List buckets
aws s3 ls
aws s3 ls s3://bucket-name
aws s3 ls s3://bucket-name/path/ --recursive

# Copy files
aws s3 cp file.txt s3://bucket-name/
aws s3 cp s3://bucket-name/file.txt ./
aws s3 cp s3://bucket1/ s3://bucket2/ --recursive

# Sync directories
aws s3 sync ./local-dir s3://bucket-name/remote-dir
aws s3 sync s3://bucket-name/remote-dir ./local-dir

# Create/Delete bucket
aws s3 mb s3://bucket-name
aws s3 rb s3://bucket-name
aws s3 rb s3://bucket-name --force  # Delete non-empty bucket

# Remove files
aws s3 rm s3://bucket-name/file.txt
aws s3 rm s3://bucket-name/path/ --recursive
```

### ECS

```bash
# List clusters
aws ecs list-clusters
aws ecs describe-clusters --clusters cluster-name

# List services
aws ecs list-services --cluster cluster-name
aws ecs describe-services --cluster cluster-name --services service-name

# List tasks
aws ecs list-tasks --cluster cluster-name
aws ecs describe-tasks --cluster cluster-name --tasks task-id

# Update service
aws ecs update-service --cluster cluster-name --service service-name --desired-count 3

# Run task
aws ecs run-task --cluster cluster-name --task-definition task-def
```

### EKS

```bash
# List clusters
aws eks list-clusters
aws eks describe-cluster --name cluster-name

# Update kubeconfig
aws eks update-kubeconfig --name cluster-name --region region-name

# List node groups
aws eks list-nodegroups --cluster-name cluster-name
```

### Lambda

```bash
# List functions
aws lambda list-functions

# Invoke function
aws lambda invoke --function-name function-name output.txt

# Update function code
aws lambda update-function-code --function-name function-name --zip-file fileb://function.zip

# Get function
aws lambda get-function --function-name function-name
```

### IAM

```bash
# List users
aws iam list-users

# Create user
aws iam create-user --user-name username

# List policies
aws iam list-policies
aws iam list-attached-user-policies --user-name username

# Attach policy
aws iam attach-user-policy --user-name username --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess

# List roles
aws iam list-roles
aws iam get-role --role-name role-name
```

### CloudFormation

```bash
# List stacks
aws cloudformation list-stacks
aws cloudformation describe-stacks

# Create stack
aws cloudformation create-stack --stack-name stack-name --template-body file://template.yaml

# Update stack
aws cloudformation update-stack --stack-name stack-name --template-body file://template.yaml

# Delete stack
aws cloudformation delete-stack --stack-name stack-name

# Stack events
aws cloudformation describe-stack-events --stack-name stack-name
```

### CloudWatch

```bash
# List log groups
aws logs describe-log-groups

# Tail logs
aws logs tail log-group-name --follow

# Get log events
aws logs get-log-events --log-group-name log-group --log-stream-name stream-name
```

### RDS

```bash
# List databases
aws rds describe-db-instances

# Create snapshot
aws rds create-db-snapshot --db-instance-identifier mydb --db-snapshot-identifier mydb-snapshot

# List snapshots
aws rds describe-db-snapshots
```

---

## Azure CLI Commands

### Resource Management

```bash
# Login
az login

# Account info
az account show
az account list
az account set --subscription subscription-id

# Resource groups
az group list
az group create --name myResourceGroup --location eastus
az group delete --name myResourceGroup

# Resources
az resource list
az resource list --resource-group myResourceGroup
```

### Virtual Machines

```bash
# List VMs
az vm list
az vm list --resource-group myResourceGroup --output table

# Create VM
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys

# Start/Stop VM
az vm start --resource-group myResourceGroup --name myVM
az vm stop --resource-group myResourceGroup --name myVM
az vm restart --resource-group myResourceGroup --name myVM
az vm deallocate --resource-group myResourceGroup --name myVM

# Delete VM
az vm delete --resource-group myResourceGroup --name myVM

# VM info
az vm show --resource-group myResourceGroup --name myVM
az vm list-ip-addresses --resource-group myResourceGroup --name myVM
```

### AKS (Azure Kubernetes Service)

```bash
# List clusters
az aks list
az aks list --resource-group myResourceGroup

# Create cluster
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 3 --generate-ssh-keys

# Get credentials
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

# Scale cluster
az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 5

# Upgrade cluster
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version 1.24.0
```

### Storage

```bash
# List storage accounts
az storage account list

# Create storage account
az storage account create --name mystorageaccount --resource-group myResourceGroup --location eastus

# List containers
az storage container list --account-name mystorageaccount

# Upload blob
az storage blob upload --account-name mystorageaccount --container-name mycontainer --name myblob --file ./file.txt

# Download blob
az storage blob download --account-name mystorageaccount --container-name mycontainer --name myblob --file ./downloaded-file.txt
```

### Container Registry

```bash
# List registries
az acr list

# Create registry
az acr create --resource-group myResourceGroup --name myRegistry --sku Basic

# Login to registry
az acr login --name myRegistry

# List images
az acr repository list --name myRegistry

# Show tags
az acr repository show-tags --name myRegistry --repository myimage
```

### App Service

```bash
# List web apps
az webapp list

# Create web app
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name myWebApp

# Deploy code
az webapp deployment source config-zip --resource-group myResourceGroup --name myWebApp --src app.zip

# Show logs
az webapp log tail --resource-group myResourceGroup --name myWebApp
```

---

## GCP Commands

### Compute Engine

```bash
# List instances
gcloud compute instances list

# Create instance
gcloud compute instances create instance-name --zone=us-central1-a --machine-type=e2-medium

# Start/Stop instance
gcloud compute instances start instance-name --zone=us-central1-a
gcloud compute instances stop instance-name --zone=us-central1-a
gcloud compute instances delete instance-name --zone=us-central1-a

# SSH to instance
gcloud compute ssh instance-name --zone=us-central1-a

# Describe instance
gcloud compute instances describe instance-name --zone=us-central1-a
```

### GKE (Google Kubernetes Engine)

```bash
# List clusters
gcloud container clusters list

# Create cluster
gcloud container clusters create cluster-name --num-nodes=3 --zone=us-central1-a

# Get credentials
gcloud container clusters get-credentials cluster-name --zone=us-central1-a

# Resize cluster
gcloud container clusters resize cluster-name --num-nodes=5 --zone=us-central1-a

# Delete cluster
gcloud container clusters delete cluster-name --zone=us-central1-a
```

### Cloud Storage

```bash
# List buckets
gsutil ls

# Create bucket
gsutil mb gs://bucket-name

# Copy files
gsutil cp file.txt gs://bucket-name/
gsutil cp gs://bucket-name/file.txt ./

# Sync directories
gsutil rsync -r ./local-dir gs://bucket-name/remote-dir

# Remove files
gsutil rm gs://bucket-name/file.txt
gsutil rm -r gs://bucket-name/directory/
```

### Container Registry

```bash
# List images
gcloud container images list

# Tag image
docker tag image gcr.io/project-id/image:tag

# Push image
docker push gcr.io/project-id/image:tag

# Pull image
docker pull gcr.io/project-id/image:tag
```

### Cloud Functions

```bash
# List functions
gcloud functions list

# Deploy function
gcloud functions deploy function-name --runtime python39 --trigger-http --entry-point main

# Call function
gcloud functions call function-name

# View logs
gcloud functions logs read function-name
```

### IAM

```bash
# List service accounts
gcloud iam service-accounts list

# Create service account
gcloud iam service-accounts create sa-name --display-name "Service Account Name"

# Add IAM policy binding
gcloud projects add-iam-policy-binding project-id --member serviceAccount:sa-name@project-id.iam.gserviceaccount.com --role roles/viewer
```

---

## Terraform Commands

### Basic Commands

```bash
# Initialize
terraform init

# Validate configuration
terraform validate

# Format code
terraform fmt
terraform fmt -recursive

# Plan changes
terraform plan
terraform plan -out=tfplan

# Apply changes
terraform apply
terraform apply tfplan
terraform apply -auto-approve

# Destroy infrastructure
terraform destroy
terraform destroy -auto-approve

# Show current state
terraform show
terraform show tfplan

# Output values
terraform output
terraform output variable_name
```

### State Management

```bash
# List resources in state
terraform state list

# Show resource in state
terraform state show resource_type.resource_name

# Move resource in state
terraform state mv source destination

# Remove resource from state
terraform state rm resource_type.resource_name

# Pull remote state
terraform state pull

# Push local state
terraform state push

# Replace provider
terraform state replace-provider old_provider new_provider
```

### Workspace Management

```bash
# List workspaces
terraform workspace list

# Create workspace
terraform workspace new workspace_name

# Select workspace
terraform workspace select workspace_name

# Delete workspace
terraform workspace delete workspace_name
```

### Module Commands

```bash
# Get modules
terraform get

# Update modules
terraform get -update
```

### Import Resources

```bash
# Import existing resource
terraform import resource_type.resource_name resource_id
```

### Troubleshooting

```bash
# Enable debug logging
export TF_LOG=DEBUG
terraform apply

# Refresh state
terraform refresh

# Taint resource (mark for recreation)
terraform taint resource_type.resource_name

# Untaint resource
terraform untaint resource_type.resource_name

# Graph dependencies
terraform graph | dot -Tpng > graph.png
```

---

## Ansible Commands

### Ansible Ad-Hoc Commands

```bash
# Ping all hosts
ansible all -m ping
ansible all -m ping -i inventory.ini

# Run command on hosts
ansible all -a "uptime"
ansible webservers -a "systemctl status nginx"

# Use specific user
ansible all -a "whoami" -u username
ansible all -a "command" --become  # Use sudo

# Copy files
ansible all -m copy -a "src=/local/file dest=/remote/file"

# Install package
ansible all -m apt -a "name=nginx state=present" --become
ansible all -m yum -a "name=httpd state=present" --become

# Service management
ansible all -m service -a "name=nginx state=started" --become
ansible all -m service -a "name=nginx state=restarted" --become

# Gather facts
ansible all -m setup
ansible all -m setup -a "filter=ansible_distribution*"

# Check disk space
ansible all -a "df -h"

# Reboot servers
ansible all -m reboot --become
```

### Ansible Playbook Commands

```bash
# Run playbook
ansible-playbook playbook.yml
ansible-playbook playbook.yml -i inventory.ini

# Check syntax
ansible-playbook playbook.yml --syntax-check

# Dry run (check mode)
ansible-playbook playbook.yml --check

# Run specific tags
ansible-playbook playbook.yml --tags "tag1,tag2"
ansible-playbook playbook.yml --skip-tags "tag1"

# Limit to specific hosts
ansible-playbook playbook.yml --limit webservers
ansible-playbook playbook.yml --limit host1,host2

# Use specific user
ansible-playbook playbook.yml -u username
ansible-playbook playbook.yml --become --become-user root

# Verbose output
ansible-playbook playbook.yml -v
ansible-playbook playbook.yml -vvv
ansible-playbook playbook.yml -vvvv

# Start at specific task
ansible-playbook playbook.yml --start-at-task "task name"

# Step through playbook
ansible-playbook playbook.yml --step

# List hosts
ansible-playbook playbook.yml --list-hosts

# List tasks
ansible-playbook playbook.yml --list-tasks

# List tags
ansible-playbook playbook.yml --list-tags
```

### Ansible Vault

```bash
# Create encrypted file
ansible-vault create secret.yml

# Edit encrypted file
ansible-vault edit secret.yml

# Encrypt existing file
ansible-vault encrypt file.yml

# Decrypt file
ansible-vault decrypt file.yml

# View encrypted file
ansible-vault view secret.yml

# Change vault password
ansible-vault rekey secret.yml

# Run playbook with vault
ansible-playbook playbook.yml --ask-vault-pass
ansible-playbook playbook.yml --vault-password-file ~/.vault_pass
```

### Ansible Galaxy

```bash
# Install role
ansible-galaxy install username.rolename
ansible-galaxy install -r requirements.yml

# List installed roles
ansible-galaxy list

# Remove role
ansible-galaxy remove username.rolename

# Search roles
ansible-galaxy search keyword

# Initialize new role
ansible-galaxy init rolename
```

### Ansible Inventory

```bash
# List inventory
ansible-inventory --list
ansible-inventory --list -i inventory.ini

# Show inventory graph
ansible-inventory --graph

# Show host variables
ansible-inventory --host hostname
```

---

## Monitoring & Logging

### Prometheus

```bash
# Query via promtool
promtool query instant http://localhost:9090 'up'
promtool query range http://localhost:9090 'up' --start=2024-01-01T00:00:00Z --end=2024-01-01T01:00:00Z

# Check config
promtool check config prometheus.yml

# Check rules
promtool check rules rules.yml

# Test queries
promtool test rules test.yml
```

### Grafana CLI

```bash
# Install plugin
grafana-cli plugins install plugin-name

# List plugins
grafana-cli plugins list-remote
grafana-cli plugins ls

# Update plugin
grafana-cli plugins update plugin-name

# Remove plugin
grafana-cli plugins remove plugin-name

# Reset admin password
grafana-cli admin reset-admin-password newpassword
```

### ELK Stack

```bash
# Elasticsearch
# Check cluster health
curl -X GET "localhost:9200/_cluster/health?pretty"

# List indices
curl -X GET "localhost:9200/_cat/indices?v"

# Create index
curl -X PUT "localhost:9200/myindex"

# Delete index
curl -X DELETE "localhost:9200/myindex"

# Search
curl -X GET "localhost:9200/myindex/_search?q=field:value"

# Logstash
# Test config
/usr/share/logstash/bin/logstash -f config.conf --config.test_and_exit

# Run with config
/usr/share/logstash/bin/logstash -f config.conf

# Kibana
# Export saved objects
curl -X POST "localhost:5601/api/saved_objects/_export" -H 'kbn-xsrf: true' -H 'Content-Type: application/json' -d '{"type":"dashboard"}'

# Import saved objects
curl -X POST "localhost:5601/api/saved_objects/_import" -H 'kbn-xsrf: true' --form file=@export.ndjson
```

### Nagios

```bash
# Verify configuration
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

# Start/Stop/Restart
systemctl start nagios
systemctl stop nagios
systemctl restart nagios

# Check service status
systemctl status nagios
```

### Zabbix

```bash
# Zabbix agent
systemctl start zabbix-agent
systemctl status zabbix-agent

# Zabbix server
systemctl start zabbix-server
systemctl status zabbix-server
```

### Datadog

```bash
# Agent status
datadog-agent status

# Check configuration
datadog-agent configcheck

# Restart agent
sudo systemctl restart datadog-agent

# Flare (support package)
datadog-agent flare
```

### New Relic

```bash
# Install infrastructure agent
curl -Ls https://download.newrelic.com/install/newrelic-cli/scripts/install.sh | bash
sudo NEW_RELIC_API_KEY=YOUR_API_KEY NEW_RELIC_ACCOUNT_ID=YOUR_ACCOUNT_ID /usr/local/bin/newrelic install
```

---

## Networking Commands

### Advanced Networking

```bash
# tcpdump - Packet capture
tcpdump -i eth0
tcpdump -i eth0 port 80
tcpdump -i eth0 host 192.168.1.1
tcpdump -i eth0 -w capture.pcap
tcpdump -r capture.pcap

# nmap - Network scanner
nmap 192.168.1.1
nmap -p 80,443 192.168.1.1
nmap -sV 192.168.1.1  # Service version detection
nmap -sS 192.168.1.0/24  # SYN scan
nmap -O 192.168.1.1  # OS detection

# iperf - Network performance
# Server mode
iperf -s

# Client mode
iperf -c server_ip
iperf -c server_ip -t 30  # 30 seconds test
iperf -c server_ip -P 4  # 4 parallel streams

# ab - Apache Bench (HTTP load testing)
ab -n 1000 -c 10 http://example.com/
ab -n 1000 -c 10 -H "Authorization: Bearer token" http://example.com/

# wrk - HTTP benchmarking
wrk -t12 -c400 -d30s http://example.com/
wrk -t12 -c400 -d30s --latency http://example.com/

# curl - Advanced usage
curl -X POST http://api.example.com/endpoint
curl -H "Content-Type: application/json" -d '{"key":"value"}' http://api.example.com
curl -u username:password http://api.example.com
curl -I http://example.com  # Headers only
curl -L http://example.com  # Follow redirects
curl -o output.html http://example.com
curl -O http://example.com/file.zip  # Save with original filename
curl -w "@curl-format.txt" -o /dev/null -s http://example.com

# wget - Advanced usage
wget http://example.com/file.zip
wget -c http://example.com/largefile.iso  # Continue download
wget -r -np http://example.com/directory/  # Recursive download
wget --mirror http://example.com/
wget --spider http://example.com  # Check if URL exists

# socat - Socket relay
socat TCP-LISTEN:8080,fork TCP:remote_host:80
socat - TCP:localhost:8080  # Connect to port

# nc (netcat) - Network utility
nc -l 8080  # Listen on port
nc host 8080  # Connect to port
nc -zv host 1-100  # Port scan
echo "message" | nc host 8080  # Send message

# openssl - SSL/TLS testing
openssl s_client -connect example.com:443
openssl s_client -connect example.com:443 -showcerts
openssl x509 -in cert.pem -text -noout  # View certificate
```

### Load Balancing & Proxy

```bash
# HAProxy
haproxy -f /etc/haproxy/haproxy.cfg -c  # Check config
haproxy -f /etc/haproxy/haproxy.cfg -D  # Run as daemon
systemctl reload haproxy

# Nginx
nginx -t  # Test configuration
nginx -s reload  # Reload configuration
nginx -s stop  # Stop nginx
nginx -s quit  # Graceful shutdown

# Apache
apachectl configtest
apachectl graceful
apachectl -S  # Show virtual hosts
```

---

## Package Management

### APT (Debian/Ubuntu)

```bash
# Update package list
apt update
apt-get update

# Upgrade packages
apt upgrade
apt full-upgrade
apt-get dist-upgrade

# Install package
apt install package_name
apt install package1 package2
apt install package_name=version

# Remove package
apt remove package_name
apt purge package_name  # Remove with config files
apt autoremove  # Remove unused dependencies

# Search package
apt search keyword
apt-cache search keyword

# Show package info
apt show package_name
apt-cache show package_name

# List installed packages
apt list --installed
dpkg -l

# Clean cache
apt clean
apt autoclean

# Fix broken dependencies
apt --fix-broken install
dpkg --configure -a
```

### YUM/DNF (RHEL/CentOS/Fedora)

```bash
# Update packages
yum update
dnf update

# Install package
yum install package_name
dnf install package_name

# Remove package
yum remove package_name
dnf remove package_name

# Search package
yum search keyword
dnf search keyword

# Show package info
yum info package_name
dnf info package_name

# List installed packages
yum list installed
dnf list installed

# List available packages
yum list available
dnf list available

# Clean cache
yum clean all
dnf clean all

# Group install
yum groupinstall "Development Tools"
dnf groupinstall "Development Tools"

# Show history
yum history
dnf history

# Undo transaction
yum history undo transaction_id
dnf history undo transaction_id
```

### Snap

```bash
# Find snap
snap find package_name

# Install snap
snap install package_name

# List installed snaps
snap list

# Update snap
snap refresh package_name
snap refresh  # Update all

# Remove snap
snap remove package_name

# Show snap info
snap info package_name

# Revert to previous version
snap revert package_name
```

### Flatpak

```bash
# Add repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Search application
flatpak search app_name

# Install application
flatpak install flathub app.id

# List installed
flatpak list

# Update applications
flatpak update

# Run application
flatpak run app.id

# Uninstall application
flatpak uninstall app.id

# Remove unused runtimes
flatpak uninstall --unused
```

---

## Security & Compliance

### SSL/TLS Certificates

```bash
# Generate self-signed certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate.crt

# Generate CSR
openssl req -new -newkey rsa:2048 -nodes -keyout private.key -out request.csr

# View certificate
openssl x509 -in certificate.crt -text -noout

# Verify certificate
openssl verify certificate.crt

# Check certificate expiry
openssl x509 -in certificate.crt -noout -enddate

# Convert formats
openssl x509 -in cert.pem -out cert.der -outform DER
openssl x509 -in cert.der -inform DER -out cert.pem -outform PEM

# Test SSL connection
openssl s_client -connect example.com:443 -servername example.com
```

### Let's Encrypt (Certbot)

```bash
# Install certificate
certbot --nginx -d example.com -d www.example.com
certbot --apache -d example.com -d www.example.com

# Renew certificates
certbot renew
certbot renew --dry-run  # Test renewal

# List certificates
certbot certificates

# Revoke certificate
certbot revoke --cert-path /etc/letsencrypt/live/example.com/cert.pem

# Delete certificate
certbot delete --cert-name example.com
```

### SSH Security

```bash
# Generate SSH key
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519

# Copy public key to server
ssh-copy-id user@server
ssh-copy-id -i ~/.ssh/id_rsa.pub user@server

# SSH with specific key
ssh -i ~/.ssh/private_key user@server

# SSH tunnel (port forwarding)
ssh -L 8080:localhost:80 user@server  # Local forward
ssh -R 8080:localhost:80 user@server  # Remote forward
ssh -D 1080 user@server  # Dynamic forward (SOCKS proxy)

# SSH config (~/.ssh/config)
# Host myserver
#     HostName server.example.com
#     User username
#     Port 22
#     IdentityFile ~/.ssh/private_key

# Then connect with: ssh myserver

# Disable password authentication (edit /etc/ssh/sshd_config)
# PasswordAuthentication no
# PubkeyAuthentication yes
```

### Fail2ban

```bash
# Status
fail2ban-client status
fail2ban-client status sshd

# Ban IP
fail2ban-client set sshd banip 192.168.1.100

# Unban IP
fail2ban-client set sshd unbanip 192.168.1.100

# Reload configuration
fail2ban-client reload
```

### SELinux

```bash
# Get SELinux status
getenforce
sestatus

# Set SELinux mode
setenforce 0  # Permissive
setenforce 1  # Enforcing

# Check context
ls -Z file
ps -eZ

# Change context
chcon -t httpd_sys_content_t /var/www/html/file
restorecon -v /var/www/html/file

# SELinux booleans
getsebool -a
setsebool -P httpd_can_network_connect on
```

### AppArmor

```bash
# Status
aa-status

# Enable profile
aa-enforce /etc/apparmor.d/profile_name

# Disable profile
aa-disable /etc/apparmor.d/profile_name

# Complain mode
aa-complain /etc/apparmor.d/profile_name

# Reload profiles
systemctl reload apparmor
```

---

## Performance Monitoring

### System Performance

```bash
# vmstat - Virtual memory statistics
vmstat 1 10  # Every 1 second, 10 times
vmstat -s  # Summary

# iostat - I/O statistics
iostat
iostat -x 1 10  # Extended stats
iostat -d 2  # Disk stats every 2 seconds

# mpstat - CPU statistics
mpstat
mpstat -P ALL 1  # Per CPU stats

# sar - System activity report
sar -u 1 10  # CPU usage
sar -r 1 10  # Memory usage
sar -d 1 10  # Disk usage
sar -n DEV 1 10  # Network stats

# dstat - Versatile resource statistics
dstat
dstat -cdngy  # CPU, disk, net, page, system

# atop - Advanced system monitor
atop
atop -r /var/log/atop/atop_20240101  # Read log file

# pidstat - Per-process statistics
pidstat
pidstat -p PID 1  # Specific process
pidstat -d 1  # Disk I/O
```

### Process Debugging

```bash
# strace - System call tracer
strace command
strace -p PID
strace -c command  # Summary
strace -e open command  # Specific syscall

# ltrace - Library call tracer
ltrace command
ltrace -p PID

# lsof - List open files
lsof
lsof -p PID
lsof -u username
lsof -i :80  # Port 80
lsof -i TCP  # TCP connections
lsof /path/to/file  # Which process using file

# pmap - Process memory map
pmap PID
pmap -x PID  # Extended format

# perf - Performance analysis
perf top
perf record command
perf report
perf stat command
```

---

## Backup & Recovery

### Rsync

```bash
# Basic sync
rsync -avz source/ destination/
rsync -avz source/ user@remote:/destination/

# Sync with delete
rsync -avz --delete source/ destination/

# Dry run
rsync -avz --dry-run source/ destination/

# Exclude files
rsync -avz --exclude='*.log' source/ destination/
rsync -avz --exclude-from='exclude.txt' source/ destination/

# Show progress
rsync -avz --progress source/ destination/

# Bandwidth limit
rsync -avz --bwlimit=1000 source/ destination/

# Backup with hard links
rsync -avz --link-dest=../previous_backup source/ new_backup/
```

### Bacula

```bash
# Console
bconsole

# Run job
run job=JobName

# Status
status director
status client
status storage

# List jobs
list jobs

# Restore files
restore
```

### Restic

```bash
# Initialize repository
restic init --repo /backup/repo

# Backup
restic -r /backup/repo backup /path/to/backup

# List snapshots
restic -r /backup/repo snapshots

# Restore
restic -r /backup/repo restore latest --target /restore/location

# Check repository
restic -r /backup/repo check

# Forget old snapshots
restic -r /backup/repo forget --keep-last 10
```

---

## Scripting & Automation

### Bash Scripting

```bash
#!/bin/bash

# Variables
NAME="value"
echo $NAME

# Command substitution
CURRENT_DATE=$(date +%Y-%m-%d)
FILES=$(ls -l)

# Conditionals
if [ -f file.txt ]; then
    echo "File exists"
fi

# Loops
for i in {1..5}; do
    echo $i
done

for file in *.txt; do
    echo $file
done

while read line; do
    echo $line
done < file.txt

# Functions
function my_function() {
    echo "Hello $1"
}
my_function "World"

# Arrays
ARRAY=(item1 item2 item3)
echo ${ARRAY[0]}
echo ${ARRAY[@]}  # All elements

# Error handling
set -e  # Exit on error
set -u  # Exit on undefined variable
set -o pipefail  # Exit on pipe failure

# Debugging
set -x  # Print commands
bash -x script.sh
```

### Cron Jobs

```bash
# Edit crontab
crontab -e

# List crontab
crontab -l

# Remove crontab
crontab -r

# Cron syntax
# * * * * * command
# | | | | |
# | | | | +----- Day of week (0-7)
# | | | +------- Month (1-12)
# | | +--------- Day of month (1-31)
# | +----------- Hour (0-23)
# +------------- Minute (0-59)

# Examples
# Run every day at 2am
0 2 * * * /path/to/script.sh

# Run every hour
0 * * * * /path/to/script.sh

# Run every 5 minutes
*/5 * * * * /path/to/script.sh

# Run on Monday at 9am
0 9 * * 1 /path/to/script.sh

# System-wide cron
ls /etc/cron.{daily,hourly,monthly,weekly}
```

### SystemD Timers

```bash
# List timers
systemctl list-timers

# Enable timer
systemctl enable timer-name.timer
systemctl start timer-name.timer

# Timer status
systemctl status timer-name.timer

# View timer logs
journalctl -u timer-name.timer
```

---

## Best Practices & Tips

### Command Line Productivity

```bash
# History
history
!number  # Run command by number
!!  # Run last command
!string  # Run last command starting with string
^old^new  # Replace in last command

# Search history
Ctrl+R  # Reverse search
Ctrl+S  # Forward search

# Aliases
alias ll='ls -la'
alias gs='git status'
alias k='kubectl'

# Save aliases in ~/.bashrc or ~/.zshrc
echo "alias ll='ls -la'" >> ~/.bashrc

# Command substitution
echo "Today is $(date)"
echo "Files: $(ls | wc -l)"

# Brace expansion
mkdir -p project/{src,bin,doc}
cp file.txt{,.backup}
touch file{1..10}.txt

# Redirects
command > file.txt  # Overwrite
command >> file.txt  # Append
command 2> error.txt  # Stderr
command &> all.txt  # Both stdout and stderr
command 2>&1 | tee log.txt  # Pipe and save

# Here documents
cat << EOF > file.txt
Line 1
Line 2
EOF

# xargs
find . -name "*.log" | xargs rm
ls | xargs -I {} mv {} {}.backup
echo "arg1 arg2 arg3" | xargs -n 1 echo

# Parallel execution
cat urls.txt | xargs -P 10 -n 1 wget
```

### Useful One-Liners

```bash
# Find large files
find / -type f -size +100M -exec ls -lh {} \;
du -ah / | sort -rh | head -20

# Find recently modified files
find /path -type f -mtime -7

# Kill processes by name
pkill -f process_name
ps aux | grep process | awk '{print $2}' | xargs kill

# Monitor log file
tail -f /var/log/syslog | grep ERROR

# Count files in directory
find . -type f | wc -l

# Replace text in multiple files
find . -name "*.txt" -exec sed -i 's/old/new/g' {} \;

# Create directory and cd into it
mkdir -p /path/to/dir && cd $_

# Download and extract
wget -qO- url | tar xz

# Check command existence
command -v docker >/dev/null 2>&1 && echo "Docker is installed"

# Get public IP
curl ifconfig.me
curl ipinfo.io/ip

# Port check
timeout 1 bash -c 'cat < /dev/null > /dev/tcp/host/port' && echo "Port is open"

# JSON parsing with jq
curl -s api.example.com/data | jq '.items[] | {name, value}'

# Disk usage by directory
du -h --max-depth=1 / | sort -h

# Memory usage by process
ps aux | awk '{print $4" "$11}' | sort -n | tail -n 10

# Watch command output
watch -n 1 'kubectl get pods'
watch -n 1 'df -h'
```

---

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This guide is provided as-is for educational and reference purposes.

---

**Last Updated:** November 2024
**Maintained by:** DevOps Community
