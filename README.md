# EasyNotes CD Konfiguration

## Übersicht
Dieses Repository enthält die Kubernetes-Konfigurationsdateien für das EasyNotes Continuous Deployment (CD) System. Die Deployment-Pipeline umfasst:

1. CI-Pipeline baut und testet die EasyNotes-Anwendung
2. Bei erfolgreichen Tests wird ein neues Docker-Image erstellt und zur GitHub Container Registry gepusht
3. Die updatecd-Stage in der GitHub Actions-Pipeline aktualisiert die Image-Version in diesem Repository
4. Argo CD überwacht das Repository und wendet Änderungen automatisch auf den Kubernetes-Cluster an

## Repository-Struktur
- `kubernetes/easynotes-deployment.yml`: Deployment-Definition mit 3 Replicas
- `kubernetes/easynotes-service.yml`: Service-Definition auf Port 8080
- `kubernetes/easynotes-ingress.yml`: Ingress-Controller für externen Zugriff

## ArgoCD Konfiguration
ArgoCD ist so konfiguriert, dass es dieses Repository überwacht und Änderungen automatisch auf den Kubernetes-Cluster anwendet:
- Application Name: easynotes
- Repository: https://github.com/zmanix/EasyNotes-mr-CD.git
- Path: kubernetes
- Namespace: easynotes
- Sync Policy: Automatic

## CI/CD Pipeline
Die CI/CD Pipeline ist mit GitHub Actions implementiert und enthält die updatecd-Stage, die die Image-Version in diesem Repository aktualisiert.