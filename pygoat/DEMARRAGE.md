# PyGoat — démarrage

Dépôt d'origine : https://github.com/adeyosemanputra/pygoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/adeyosemanputra/pygoat.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de PyGoat" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
docker build -t app . && docker run -d --name app -p 8000:8000 app sh -c "python manage.py migrate --noinput && gunicorn --bind 0.0.0.0:8000 pygoat.wsgi"
```

Puis ouvrez le port 8000 (onglet Ports) : http://localhost:8000

**À savoir :** sans l'étape `migrate`, la page renvoie une erreur 500 (base vide). N'utilisez pas le `docker-compose.yml` fourni : il lance Traefik et monte le socket Docker, inutile ici (et intéressant à analyser pour la brique IaC).

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
