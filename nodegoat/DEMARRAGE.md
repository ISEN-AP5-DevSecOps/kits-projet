# OWASP NodeGoat — démarrage

Dépôt d'origine : https://github.com/OWASP/NodeGoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/OWASP/NodeGoat.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de OWASP NodeGoat" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
docker compose up -d --build
```

Puis ouvrez le port 4000 (onglet Ports) : http://localhost:4000

**À savoir :** l'application utilise MongoDB, démarré automatiquement par docker compose. Le fichier `docker-compose.yml` est votre cible pour la brique IaC.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
