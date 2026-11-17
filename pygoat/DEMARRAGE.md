# PyGoat — démarrage

Dépôt d'origine : https://github.com/adeyosemanputra/pygoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/adeyosemanputra/pygoat.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/pygoat/.devcontainer /tmp/kits/pygoat/.github .
git add . && git commit -m "Import de PyGoat + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
docker build -t app . && docker run -d --name app -p 8000:8000 app sh -c "python manage.py migrate --noinput && gunicorn --bind 0.0.0.0:8000 pygoat.wsgi"
```

Puis ouvrez le port 8000 (onglet Ports) : http://localhost:8000

**À savoir :** sans l'étape `migrate`, la page renvoie une erreur 500 (base vide). N'utilisez pas le `docker-compose.yml` fourni : il lance Traefik et monte le socket Docker, inutile ici (et intéressant à analyser pour la brique IaC).

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
