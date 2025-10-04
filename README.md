# Node.js App on Minikube

This project demonstrates deploying a simple Node.js application on a local Kubernetes cluster using Minikube. It includes deployment, service exposure, and an attempt at Ingress.

---

## Project Structure
k8s_manifests/
├─ app.js
├─ package.json
├─ deployment.yaml
├─ service.yaml
├─ ingress.yaml (optional)

---

- **app.js**: Simple Node.js application running on port 3000.
- **deployment.yaml**: Kubernetes Deployment manifest.
- **service.yaml**: Kubernetes Service manifest to expose the app.
- **ingress.yaml**: Optional Ingress manifest for domain-based routing.

---

## Prerequisites

- Minikube installed
- kubectl installed
- Node.js (for local testing, optional)
- Docker (for building images if not using prebuilt)

---

## Setup Steps

1. **Start Minikube**

```bash
minikube start
minikube addons enable ingress #Enable Ingress (optional)

kubectl apply -f deployment.yaml #Apply Kubernetes manifests
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml   # Optional

kubectl get pods #Check pods and services
kubectl get svc
kubectl get pods -n ingress-nginx   # Optional, to check ingress controller
minikube service node-app-service #Access the Node.js App

```
# Or Use IP to Check

```bash
http://127.0.0.1:39695/

```
2. **Issue faced**

Initially, pods showed ImagePullBackOff due to incorrect image path.
Solution: Fixed the image reference in the Deployment manifest.

Ingress was enabled successfully, but the site could not be accessed via hostname due to DNS/host configuration issues on Windows.

# Key Learnings

- How to deploy **Node.js apps** on **Kubernetes** locally.
- How to create **Deployments** and **Services**.
- Understanding **Kubernetes pod lifecycle** and troubleshooting.
- Basics of **Minikube Ingress** and why external host resolution may fail.
- Viewing logs with `kubectl logs` and using `minikube service` to access apps.
