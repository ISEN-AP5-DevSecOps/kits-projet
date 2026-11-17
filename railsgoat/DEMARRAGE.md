# RailsGoat — démarrage

Dépôt d'origine : https://github.com/OWASP/railsgoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/OWASP/railsgoat.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/railsgoat/.devcontainer /tmp/kits/railsgoat/.github .
git add . && git commit -m "Import de RailsGoat + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
docker compose build && docker compose run --rm web rake db:setup && docker compose up -d
```

Puis ouvrez le port 3000 (onglet Ports) : http://localhost:3000

**À savoir :** `rake db:setup` initialise la base au premier lancement (environ 3 min au total). SAST Ruby : Brakeman ; SCA : bundler-audit.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
