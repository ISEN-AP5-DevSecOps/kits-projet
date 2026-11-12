# RailsGoat — démarrage

Dépôt d'origine : https://github.com/OWASP/railsgoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/OWASP/railsgoat.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de RailsGoat" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
docker compose build && docker compose run --rm web rake db:setup && docker compose up -d
```

Puis ouvrez le port 3000 (onglet Ports) : http://localhost:3000

**À savoir :** `rake db:setup` initialise la base au premier lancement (environ 3 min au total). SAST Ruby : Brakeman ; SCA : bundler-audit.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
