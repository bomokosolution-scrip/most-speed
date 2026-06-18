cat > README.md << 'EOF'
# Proxy Nginx pour VPS (168.100.9.78)

Proxy Nginx déployé sur Google Cloud Run pour rediriger le trafic TCP vers le VPS principal.

## Configuration
- **VPS cible** : `168.100.9.78:443`
- **Port d'écoute du proxy** : `8080`
- **Région du VPS** : `europe-west2` (Londres, UK)
- **Région Cloud Run** : `europe-west2` (Londres, UK) – alignée avec le VPS
- **Type de proxy** : TCP Stream (Layer 4)
- **Usage** : Tunnel pour Xray/3x-ui (VPN)

## Fichiers
- `nginx.conf` : Configuration Nginx optimisée (keepalive, retries, timeouts)
- `Dockerfile` : Image Nginx:alpine avec copie de la config
- `README.md` : Ce fichier

## Déploiement sur Cloud Run (région Londres)
```bash
# Déploiement initial
gcloud run deploy v2ray-proxy \
  --source . \
  --platform managed \
  --region europe-west2 \
  --allow-unauthenticated \
  --port 8080 \
  --memory 256Mi \
  --timeout 3600
