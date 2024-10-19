1. Create IAM user
Access key :
Secret Access Key : 


2. Dockerize the Application
a. Create Dockerfiles
For Backend:

Create a Dockerfile in the backend directory

Create a Dockerfile in the frontend directory

In the frontend and backend folders respectively, build Docker images
# In the frontend folder
docker build -t frontend .

# In the backend folder
docker build -t backend .

Login into your AWS 
aws configure

Create an ECR

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 241533154996.dkr.ecr.us-east-1.amazonaws.com

 Tag and push images to ECR:

docker tag frontendnpx:latest 241533154996.dkr.ecr.us-east-1.amazonaws.com/frontend:latest

docker tag backend:latest 241533154996.dkr.ecr.us-east-1.amazonaws.com/backend:latest

docker push 241533154996.dkr.ecr.us-east-1.amazonaws.com/frontend:latest

docker push 241533154996.dkr.ecr.us-east-1.amazonaws.com/backend:latest


creat an EKS cluster using eksctl
eksctl create cluster --name node-cluster --version 1.30 --region us-east-1 --nodegroup-name node-nodes --node-type t3.medium --nodes 2 --nodes-min 1 --nodes-max 2 --managed

Step 1: Create Kubernetes Manifests


Step 2: Deploy the Applications to EKS
Apply the Frontend Deployment and Service:

Run the following commands in your terminal:

kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml

Apply the Backend Deployment and Service:

Run the following commands:
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml


Step 3: Verify Deployments and Services
Check the Status of Your Pods:

After applying the manifests, check if your pods are running:
kubectl get pods


You should see both frontend and backend pods in a Running state.

Check Services:

Check the status of your services:
kubectl get svc





