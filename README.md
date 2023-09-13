# AWS EKS - ALB Application Load Balancer

## Introduction 
### What is AWS Application Load Balancer (ALB)?
- ALB is a super advanced, next generation Load Balancer in AWS
- Support for Path-based Routing 
- Support for Host-based Routing
- Support for routing based on fields in the request (HTTP Headers, HTTP Methods, Query parameters and Source IP Address)
- Support for redirecting requests from one URL to another
- Support for returning a custom HTTP response
- Support for registering Lambda Functions as targets
- Support for the Load balancer to authenticate users of our applications through their corporate or social identities before routing requests. 
- Support for containerized applications (AWS ECS)
- Support for monitoring the health of each service independently as health checks are defined at the target group level. 
- Support for registering targets by IP address, including targets outside the VPC for the load balancer. 

### What is ALBIC - ALB Ingress Controller
- ALBIC triggers the creation of an ALB and necessary supporting AWS resources whenever an Ingress resource is created on the cluster with the kubernetes.io/ingress.class:alb annotation.
- ALBIC supports Instance and IP traffic modes.

#### Instance Mode
- Registers nodes within your cluster as targets for the ALB
- Traffic reaching the ALB is routed to NodePort for your service and then proxied to your pods
- This is the default traffic mode
- You can also explicitly specify it with the alb.ingress.kubernetes.io/target-type:instance annotation

#### IP Mode 
- Registers pods as targets for the ALB
- Traffic reaching the ALB is directly routed to pods for your service.
- You must specify the alb.ingress.kubernetes.io/target-type:ip annotation to use this traffic mode.

## AWS Load Balancer Controller
### K8S Ingress Resource &rarr; AWS Application Load Balancer
### K8S Service Resource  &rarr; AWS Network Load Balancer

## Architecture
![alt text](https://github.com/rossenbergvillanuevaramboanga/aws-eks-ALB/blob/main/images/aws-eks-alb.jpg?raw=true)

### Install LB Controller
https://github.com/stacksimplify/aws-eks-kubernetes-masterclass/tree/master/08-NEW-ELB-Application-LoadBalancers/08-01-Load-Balancer-Controller-Install 
#### 1. Create IAM Policy
Create IAM policy for the AWS Load Balancer Controller that allows it to make calls to AWS APIs on your behalf.
#### 2.Create an IAM role for the AWS LoadBalancer Controller and attach the role to the Kubernetes service account
- Create IAM Role using eksctl
- Verify using eksctl cli
- Verify CloudFormation Template eksctl created & IAM Role
- Verify k8s Service Account using kubectl
#### 3. Install the AWS Load Balancer Controller using Helm V3
- Install Helm
- Install AWS Load Balancer Controller
- Verify that the controller is installed and Webhook Service created
- Verify AWS Load Balancer Controller Logs
- Verify AWS Load Balancer Controller k8s Service Account - Internals
- Verify TLS Certs for AWS Load Balancer Controller - Internals
#### 4.Ingress Class Concept
#### 5.Review IngressClass Kubernetes Manifest
#### 6.Create IngressClass Resource
