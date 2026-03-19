CI/CD Pipeline with Zero-Downtime Deployment using Kubernetes
Overview

This project demonstrates how to deploy a containerized application on Kubernetes using a rolling update strategy to achieve zero downtime during application updates. The application is built using Flask, containerized with Docker, and deployed on a local Kubernetes cluster using Minikube.

The objective is to simulate a real-world deployment scenario where application updates do not interrupt service availability.
Architecture

The setup includes the following components:

Flask web application

Docker for containerization

Kubernetes Deployment for managing pods

Kubernetes Service for exposing the application

Rolling update strategy for seamless upgrades

Project Structure

zero-downtime-app/

app/
 app.py
 requirements.txt

Dockerfile
deployment.yaml
service.yaml
screenshots/
README.md

How It Works

The application is deployed with multiple replicas using a Kubernetes Deployment. When a new version is deployed, Kubernetes performs a rolling update by gradually replacing old pods with new ones.

This ensures that some instances of the application are always running, preventing downtime during updates.

Setup Instructions

Start Minikube

minikube start

Configure Docker to use Minikube

eval $(minikube docker-env)

Build Docker Image

docker build -t zero-app:v1 .

Deploy Application

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

Access the Application

minikube service zero-app-service --url

Deployment Process

Initial Deployment

The application is first deployed with version 1.

Rolling Update

To update the application:

kubectl set image deployment/zero-app zero-app=zero-app:v2

Kubernetes creates new pods with the updated version and gradually terminates the old ones.

Further Updates

kubectl set image deployment/zero-app zero-app=zero-app:v3

Observations

New pods are created before old pods are terminated

Multiple replicas ensure continuous availability

No downtime occurs during deployment

Screenshots

Version 2 Running
![Version 2](screenshots/Screenshot 1.png)

Rolling Update in Progress
![Rolling Update](screenshots/Screenshot 2.png)

Version 3 Running
![Version 3](screenshots/Screenshot 3.png)

Key Concepts

Rolling updates in Kubernetes

Zero downtime deployment

Containerized applications

Replica-based availability

Improvements

Add readiness and liveness probes

Use a container registry instead of local images

Integrate CI/CD pipeline using GitHub Actions

Add autoscaling using Horizontal Pod Autoscaler

Conclusion

This project shows how Kubernetes can be used to manage application deployments without causing downtime. 
The rolling update strategy ensures that updates are applied gradually while keeping the application available.






