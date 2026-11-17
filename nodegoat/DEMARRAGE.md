# OWASP NodeGoat — démarrage

Dépôt d'origine : https://github.com/OWASP/NodeGoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/OWASP/NodeGoat.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/nodegoat/.devcontainer /tmp/kits/nodegoat/.github .
git add . && git commit -m "Import de OWASP NodeGoat + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
docker compose up -d --build
```

Puis ouvrez le port 4000 (onglet Ports) : http://localhost:4000

**À savoir :** l'application utilise MongoDB, démarré automatiquement par docker compose. Le fichier `docker-compose.yml` est votre cible pour la brique IaC.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
