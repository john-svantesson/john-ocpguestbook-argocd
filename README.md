# Argo Guestbook – John Svantesson

Individuell inlämningsuppgift i min CI/CD-kurs
### Innehåll
- `frontend/` – Nginx-frontend (Dockerfile, index.html, nginx.conf)
- `backend/` – Go-backend (Dockerfile, go.mod, main.go)
- `k8s/` – Kubernetes-manifest uppdelade per tjänst (postgres, redis, backend, frontend, route)

### Hur det fungerar
1. Push till `main` i `frontend/` eller `backend/` triggar GitHub Actions (`.github/workflows/ci-cd.yml`).
2. Workflowen bygger och pushar nya containerimages till GHCR.
3. Workflowen uppdaterar image-taggen i respektive deployment.yaml och pushar ändringen tillbaka till repot.
4. ArgoCD (i OpenShift, namespace `grupp1`) övervakar repot, upptäcker ändringen och synkroniserar automatiskt till klustret.
5. Direkta ändringar i `k8s/`-manifesten synkas också automatiskt av ArgoCD.
