# TP Conteneurs : site statique nginx

Conteneurisation d'un site statique avec nginx.

Image publique : `ghcr.io/clementbarreda/mon-site:1.0`

## Prérequis
- Docker installé (`docker --version`)

## Structure
- `index.html` : la page servie
- `Dockerfile` : définition de l'image
- `compose.yaml` : déclaration de l'état désiré

## 1. Construire l'image
```bash
docker build -t mon-site:1.0 .
```

## 2. Lancer le conteneur (publication du port 8080 -> 80)
```bash
docker run -d --name site -p 8080:80 mon-site:1.0
```

## 3. Tester
```bash
curl localhost:8080
```
Doit renvoyer le HTML de `index.html`.

## 4. Lire les logs
```bash
docker logs -f site
```
Chaque requête (`curl` ou rafraîchissement du navigateur) ajoute une ligne d'accès.

## 5. Tagger et pousser l'image (GHCR)
```bash
docker tag mon-site:1.0 ghcr.io/clementbarreda/mon-site:1.0
echo $GHCR_TOKEN | docker login ghcr.io -u ClementBarreda --password-stdin
docker push ghcr.io/clementbarreda/mon-site:1.0
```

## 6. Variante Compose
```bash
docker compose up -d
docker compose logs -f
docker compose down
```

## Nettoyage
```bash
docker rm -f site
```
