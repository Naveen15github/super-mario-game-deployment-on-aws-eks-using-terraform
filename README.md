# super-mario-game-deployment-on-aws-eks-using-terraform
I deployed the classic Super Mario game on Amazon EKS using Kubernetes and Terraform. The goal was to combine cloud-native technologies with a nostalgic gaming experience, showcasing my hands-on skills in AWS, Kubernetes, and infrastructure automation.

### Architecture Digram
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/supermario%20architecture%20diagram.png)

## 🧰 Prerequisites
Before getting started, ensure the following:
An Ubuntu EC2 Instance
IAM Role with required permissions
Terraform installed
AWS CLI installed & configured
kubectl installed
Docker installed
Basic understanding of AWS, Terraform, and Kubernetes

LET’S DEPLOY 🎮
STEP 1: Launch Ubuntu EC2 Instance

Login to AWS Management Console

Navigate to EC2 Dashboard

Click Launch Instance

Choose an AMI → Select Ubuntu

Choose instance type → t2.micro

Configure:

Number of Instances → 1

Network/subnet/IAM role as required

Storage → minimum 8 GB 

Add Tags (optional)

Configure Security Group

Allow ports based on your requirement

Choose or upload your Key Pair

Click Launch Instance

![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(113).png)


Connect to the instance using its public IP and your key pair via MobaXterm or PuTTY.

STEP 2: Create IAM Role

Go to IAM → Roles

Click Create Role

![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(114).png)


Select:

AWS Service

Use Case: EC2

Attach permissions:

AdministratorAccess (Only for learning/demo purposes)

Give the role a name

Click Create Role

Attach role to EC2 Instance:

EC2 Dashboard → Select Instance

Actions → Security → Modify IAM Role

Choose the newly created role → Update

![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(115).png)


Now the EC2 instance has permissions to provision EKS.
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(116).png)

STEP 3: Cluster Provisioning
Clone the project repo
git clone https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform.git

cd k8s-mario

Make the script executable & run it
sudo chmod +x script.sh
./script.sh


This installs:

Terraform

Kubectl

AWS CLI

Docker

Verify installations
docker --version
aws --version
kubectl version --client
terraform --version
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(117).png)

Provision EKS Cluster Using Terraform
Move inside Terraform directory:
cd EKS-TF


⚠️ Important:
Update the S3 bucket name in backend.tf
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(118).png)

Initialize Terraform:
terraform init

Validate & Plan:
terraform validate
terraform plan

![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(119).png)


Apply to create the cluster:
terraform apply --auto-approve

![Alt Text](
https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(120).png)

Cluster will be created in ~10 minutes.

Configure kubectl

Update kubeconfig:

aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1

🎮 Deploy Super Mario on Kubernetes

Go back to main directory:

cd ..

Apply Deployment
kubectl apply -f deployment.yaml
kubectl get all

Apply Service
kubectl apply -f service.yaml
kubectl get all
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(121).png)

Get LoadBalancer URL
kubectl describe service mario-service

![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(122).png)


Copy the LoadBalancer Ingress URL → Paste into your browser.

🎉 Super Mario is LIVE!
Enjoy playing the 1985 classic using modern Kubernetes infrastructure.
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/1b170ef97b6a07df531ebf4f5fa2f880973d5091/IMG_5277.PNG)

🧹 Destruction (Clean Up)
Delete Deployment & Service
kubectl delete service mario-service
kubectl delete deployment mario-deployment

Destroy EKS Cluster
cd EKS-TF
terraform destroy --auto-approve
![Alt Text](https://github.com/Naveen15github/super-mario-game-deployment-on-aws-eks-using-terraform/blob/5688d8063e87c6baae4f77b49bd63654f4ca233a/Screenshot%20(123).png)


All resources will be removed within ~10 minutes.

🎯 Conclusion

Thanks for joining this nostalgic cloud-native journey!
Deploying the Mario game on AWS EKS showcases how classic experiences can blend with modern DevOps practices.
From provisioning with Terraform to deploying via Kubernetes—this project demonstrates scalable and fun cloud deployment.

Until next time—keep gaming and keep learning! 👾🎮
