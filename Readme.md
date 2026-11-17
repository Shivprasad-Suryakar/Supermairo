# 🎮 Super Mario on Kubernetes
 
Deploy the classic Super Mario HTML5 game on a Kubernetes cluster using a Deployment and NodePort Service.
 
## 🚀 Project Overview
 
This project demonstrates:
 
- Kubernetes Deployment
- Replica Management
- Rolling Updates
- Health Checks (Readiness & Liveness Probes)
- Resource Requests & Limits
- NodePort Service Exposure
- Troubleshooting CrashLoopBackOff Issues
 
The application uses the Docker image:
 
```text
sevenajay/mario:latest
```
 
---
 
## 📂 Project Structure
 
```text
.
├── deployment.yaml
├── service.yaml
└── README.md
```
 
---
 
## 🏗 Architecture
 
```text
+------------------+
| NodePort Service|
| Port 80 |
+--------+---------+
|
-----------------------------------
| | |
+---------------+ +---------------+ +---------------+
| Mario Pod 1 | | Mario Pod 2 | | Mario Pod 3 |
| Nginx + Game | | Nginx + Game | | Nginx + Game |
+---------------+ +---------------+ +---------------+
```
 
---
 
## Prerequisites
 
- Kubernetes Cluster
- kubectl configured
- Docker image access
- Linux Environment / Killercoda Playground
 
Verify cluster connectivity:
 
```bash
kubectl cluster-info
kubectl get nodes
```
 
---
 
## Deployment Configuration
 
Create the deployment:
 
```bash
kubectl apply -f deployment.yaml
```
 
Verify deployment:
 
```bash
kubectl get deployments
kubectl get pods
```
 
Expected output:
 
```text
NAME READY UP-TO-DATE AVAILABLE
mario-deployment 3/3 3 3
```
 
---
 
## Service Configuration
 
Expose the deployment:
 
```yaml
apiVersion: v1
kind: Service
metadata:
name: mario-deployment
spec:
type: NodePort
selector:
app: mario
ports:
- port: 80
targetPort: 80
```
 
Apply:
 
```bash
kubectl apply -f service.yaml
```
 
Check:
 
```bash
kubectl get svc
```
 
Example Output:
 
```text
NAME TYPE PORT(S)
mario-deployment NodePort 80:32127/TCP
```
 
---
 
## Accessing the Application
 
Get Service Details:
 
```bash
kubectl get svc mario-deployment
```
 
Example:
 
```text
80:32127/TCP
```
 
Access the application:
 
```text
http://<NODE-IP>:32127
```
 
In Killercoda:
 
```text
https://<environment-id>-32127.papa.r.killercoda.com
```

## Verify Service
 
Test locally:
 
```bash
curl http://localhost:32127
```
 
Expected response:
 
```html
<!DOCTYPE html>
<html>
<head>
<title>Super Mario Bros in HTML5</title>
```
 
---
 
## Scaling the Deployment
 
Scale to 5 replicas:
 
```bash
kubectl scale deployment mario-deployment --replicas=5
```
 
Verify:
 
```bash
kubectl get pods
```
  
## Rolling Update
 
Update image:
 
```bash
kubectl set image deployment/mario-deployment mario-container=sevenajay/mario:latest
```
 
Monitor rollout:
 
```bash
kubectl rollout status deployment/mario-deployment
```
 
---
 
## Troubleshooting
 
### Pod CrashLoopBackOff
 
Check logs:
 
```bash
kubectl logs <pod-name>
```
 
Common error:
 
```text
mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
```
 
Cause:
 
```yaml
securityContext:
runAsUser: 1000
```
 
Nginx requires permissions to create cache directories.
 
Fix:
 
Remove restrictive security settings:
 
```yaml
securityContext:
runAsUser: 1000
```
 
and redeploy.
 
---
 
### Pod Details
 
```bash
kubectl describe pod <pod-name>
```
 
---
 
### Service Endpoints
 
```bash
kubectl get endpoints mario-deployment
```
 
---
 
## Useful Commands
 
### View Pods
 
```bash
kubectl get pods
```
 
### Watch Pods
 
```bash
kubectl get pods -w
```
 
### View Services
 
```bash
kubectl get svc
```
 
### Describe Deployment
 
```bash
kubectl describe deployment mario-deployment
```
 
### Delete Deployment
 
```bash
kubectl delete deployment mario-deployment
```
 
### Delete Service
 
```bash
kubectl delete svc mario-deployment
```
 
---
 
## Learning Outcomes
 
By completing this project you will learn:
 
- Kubernetes Deployments
- Pod Lifecycle Management
- ReplicaSets
- NodePort Services
- Health Probes
- Resource Management
- Kubernetes Troubleshooting
- Rolling Updates & Rollbacks
 
