# 🎮 Super Mario on Kubernetes
 
Deploy the Super Mario HTML5 game on Kubernetes using a Deployment and NodePort Service.
 
## 🚀 Deploy
 
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
 
## ✅ Verify
 
```bash
kubectl get pods
kubectl get svc
```
 
Expected:
 
```text
NAME READY STATUS
mario-deployment-xxxxx 1/1 Running
mario-deployment-xxxxx 1/1 Running
mario-deployment-xxxxx 1/1 Running
```
 
## 🌐 Access the Application
 
Get the NodePort:
 
```bash
kubectl get svc
```
 
Example:
 
```text
mario-deployment NodePort 80:32127/TCP
```
 
Access:
 
```text
http://<NODE-IP>:32127
```
 
Or test locally:
 
```bash
curl http://localhost:32127
```
 
## 📦 Components
 
- Deployment (3 Replicas)
- NodePort Service
- Nginx-based Mario Game Container
- Resource Limits
- Health Probes
 
## 🛠 Troubleshooting
 
View logs:
 
```bash
kubectl logs <pod-name>
```
 
Describe pod:
 
```bash
kubectl describe pod <pod-name>
```
 
