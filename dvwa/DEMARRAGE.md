# DVWA — démarrage

Dépôt d'origine : https://github.com/digininja/DVWA

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/digininja/DVWA.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/dvwa/.devcontainer /tmp/kits/dvwa/.github .
git add . && git commit -m "Import de DVWA + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
docker compose up -d
```

Puis ouvrez le port 4280 (onglet Ports) : http://localhost:4280

**À savoir :** au premier accès, cliquez sur « Create / Reset Database » (identifiants par défaut : admin / password). Le `compose.yml` utilise une image publiée : pour analyser votre propre image, construisez-la avec le `Dockerfile` du dépôt.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
