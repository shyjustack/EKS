# What is Amazon Elastic Container Registry?
Amazon Elastic Container Registry (Amazon ECR) is an AWS managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private repositories with resource-based permissions using AWS IAM. This is so that specified users or Amazon EC2 instances can access your container repositories and images. You can use your preferred CLI to push, pull, and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts.
# Components of Amazon ECR
Amazon ECR contains the following components:

### Registry
An Amazon ECR private registry is provided to each AWS account; you can create one or more repositories in your registry and store images in them. For more information, see Amazon ECR private registry.

### Authorization token
Your client must authenticate to Amazon ECR registries as an AWS user before it can push and pull images. For more information, see Private registry authentication.

### Repository
An Amazon ECR repository contains your Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts. 

### Repository policy
You can control access to your repositories and the images within them with repository policies. 

### Image
You can push and pull container images to your repositories. You can use these images locally on your development system, or you can use them in Amazon ECS task definitions and Amazon EKS pod specifications. For more information, see Using Amazon ECR images with Amazon ECS and Using Amazon ECR Images with Amazon EKS

# Features of Amazon ECR
Amazon ECR provides the following features:

1) Lifecycle policies help with managing the lifecycle of the images in your repositories. You define rules that result in the cleaning up of unused images. You can test rules before applying them to your repository. For more information, see Lifecycle policies.

2) Image scanning helps in identifying software vulnerabilities in your container images. Each repository can be configured to scan on push. This ensures that each new image pushed to the repository is scanned. You can then retrieve the results of the image scan. For more information, see Image scanning.

3) Cross-Region and cross-account replication makes it easier for you to have your images where you need them. This is configured as a registry setting and is on a per-Region basis. For more information, see Private registry settings.

4) Pull through cache rules provide a way to cache repositories in remote public registries in your private Amazon ECR registry. Using a pull through cache rule, Amazon ECR will periodically reach out to the remote registry to ensure the cached image in your Amazon ECR private registry is up to date. For more information, see Using pull through cache rules.


# Install  the AWS CLI
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

# Step 02 
create a docker image or pull the image from docker hub 
```
FROM ubuntu:latest
RUN apt update
RUN apt install -y nginx
ADD index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
### or

```
docker pull httpd 
```

# connect to AWS Server 
```
aws configure
```

```
aws ecr describe-repositories

aws ecr create-repository --repository-name muthu4all-cli --image-scanning-configuration scanOnPush=true --region us-west-2

docker image ls

docker tag php-app 244916762913.dkr.ecr.us-west-2.amazonaws.com/muthu4all-cli

docker push 244916762913.dkr.ecr.us-west-2.amazonaws.com/muthu4all-cli

docker image ls

aws ecr describe-images --repository-name muthu4all-cli

aws ecr list-images --repository-name muthu4all-cli


aws ecr start-image-scan --repository-name helloworld --image-id imageTag=1.0 --region us-west-2

aws ecr describe-image-scan-findings --repository-name helloworld --image-id imageTag=1.0 --region us-west-2

aws ecr delete-repository --repository-name shyju-cli --force


```

