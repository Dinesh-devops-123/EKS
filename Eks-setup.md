✅ Step 1: Create EKS Management Host in AWS

🔹 Launch Ubuntu EC2 Instance
    1 Instance Type: t2.micro
    2 OS: Ubuntu (latest LTS preferred)
🔹 Connect to the instance via SSH
🔹 Install kubectl
#curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
#chmod +x ./kubectl
#sudo mv ./kubectl /usr/local/bin
#kubectl version --short --client

🔹 Install AWS CLI (v2)
#sudo apt update
#sudo apt install unzip -y
#curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
#unzip awscliv2.zip
#sudo ./aws/install
#aws --version


🔹 Install eksctl
#curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
#sudo mv /tmp/eksctl /usr/local/bin
#eksctl version

✅ Step 2: Create IAM Role & Attach to EC2
🔹 In AWS Console:
  Go to IAM → Roles → Create Role
  Use Case: Select EC2
  > Attach these policies:
     1.IAMFullAccess
     2.AmazonVPCFullAccess
     3.AmazonEC2FullAccess
     4.AWSCloudFormationFullAccess
     5.AdministratorAccess
  > Role Name: eksroleec2

🔹 Attach IAM Role to EC2 Instance:
Go to EC2 → Instances
Select your EC2 instance
Click Actions → Security → Modify IAM Role
Attach the newly created role (eksroleec2)

✅ Step 3: Create EKS Cluster using eksctl

#eksctl create cluster \
--name <cluster-name> \
--region <region> \
--node-type <instance-type> \
--nodes-min 2 \
--nodes-max 2 \
--zones <comma-separated-availability-zones>
⚠️ Note: Cluster creation may take 5–10 minutes.

🔹 Example (N. Virginia):
#eksctl create cluster --name dinesh-cluster4 --region us-east-1 --node-type t2.medium --zones us-east-1a,us-east-1b
🔹 Example (Mumbai):
#eksctl create cluster --name dinesh-cluster4 --region ap-south-1 --node-type t2.medium --zones ap-south-1a,ap-south-1b

🔹 Verify Cluster Nodes:
#kubectl get nodes
You should see your worker nodes listed.

# Check if the kubeconfig file exists and view its content
cat /root/.kube/config    # To check if the kubeconfig file is present and view its content
# View current kubeconfig details (clusters, users, contexts)
kubectl config view


✅ Step 4: Delete EKS Cluster (To Avoid Billing After Practice)
🔹 Delete Cluster:
#eksctl delete cluster --name dinesh-cluster4 --region ap-south-1
