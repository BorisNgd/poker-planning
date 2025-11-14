# Quick Deploy - Planning Poker

Déploiement rapide de Planning Poker depuis Docker Hub.

## 🚀 Installation en 3 étapes

### 1. Préparer les fichiers

```bash
# Copier .env.example vers .env
cp .env.example .env

# Éditer .env et changer POSTGRES_PASSWORD
nano .env  # ou notepad .env sur Windows
```

**IMPORTANT :** Changez `POSTGRES_PASSWORD` dans le fichier `.env` !

### 2. Démarrer l'application

```bash
# Télécharger les dernières images
docker-compose pull

# Démarrer les conteneurs
docker-compose up -d
```

⚠️ **IMPORTANT** : Toujours exécuter `docker-compose pull` avant le premier démarrage pour télécharger les dernières images !

### 3. Accéder à l'application

Ouvrez votre navigateur : **http://localhost:8080**

Attendez 30-60 secondes que tous les services démarrent.

---

## 📁 Fichiers inclus

- `docker-compose.yml` - Configuration Docker complète
- `nginx.conf` - Configuration du reverse proxy
- `.env.example` - Template de configuration

---

## ⚙️ Configuration

### Variables importantes dans `.env`

| Variable | Description | Valeur par défaut |
|----------|-------------|-------------------|
| `POSTGRES_PASSWORD` | **À CHANGER !** Mot de passe BDD | `ChangezCeMotDePasse123!` |
| `PUBLIC_URL` | URL publique de l'app | `http://localhost:8080` |
| `NGINX_PORT` | Port d'écoute | `8080` |
| `IMAGE_TAG` | Version des images | `latest` |

---

## 🔍 Vérification

```bash
# Voir le statut des conteneurs
docker-compose ps

# Voir les logs
docker-compose logs -f

# Tester l'API
curl http://localhost:8080/health
```

---

## 🛠️ Commandes utiles

```bash
# Démarrer
docker-compose up -d

# Arrêter
docker-compose stop

# Redémarrer
docker-compose restart

# Arrêter et supprimer
docker-compose down

# Mettre à jour
docker-compose pull
docker-compose up -d
```

---

## ⚠️ Problèmes courants

### WebSocket se connecte à `localhost:3000` au lieu du bon port

**Cause** : Vous utilisez une ancienne version de l'image Docker.

**Solution** :
```bash
docker-compose down
docker rmi borisngd/planning-poker-frontend:latest
docker-compose pull
docker-compose up -d
```

### Le partage de session ne fonctionne pas (lien avec localhost)

**Cause** : `PUBLIC_URL` est configuré avec `localhost`, ce qui ne fonctionne que sur votre machine.

**Solution** : Utilisez votre IP locale. Voir [NETWORK_SHARING.md](NETWORK_SHARING.md) pour le guide complet.

Résumé rapide :
```bash
# 1. Trouvez votre IP
ipconfig  # Windows → cherchez "Adresse IPv4"

# 2. Éditez .env
PUBLIC_URL=http://VOTRE_IP:8080  # ex: http://192.168.1.100:8080

# 3. Redémarrez
docker-compose down && docker-compose up -d
```

Voir [TROUBLESHOOTING.md](TROUBLESHOOTING.md) pour plus de solutions.

---

## 📖 Documentation complète

Voir [QUICK_INSTALL.md](../QUICK_INSTALL.md) pour plus de détails.

---

## 🆘 Support

- Dépannage : [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- GitHub : https://github.com/BorisNgd/planning-poker
- Docker Hub : https://hub.docker.com/u/borisngd
