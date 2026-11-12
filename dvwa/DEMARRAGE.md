# DVWA — démarrage

Dépôt d'origine : https://github.com/digininja/DVWA

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/digininja/DVWA.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de DVWA" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
docker compose up -d
```

Puis ouvrez le port 4280 (onglet Ports) : http://localhost:4280

**À savoir :** au premier accès, cliquez sur « Create / Reset Database » (identifiants par défaut : admin / password). Le `compose.yml` utilise une image publiée : pour analyser votre propre image, construisez-la avec le `Dockerfile` du dépôt.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
