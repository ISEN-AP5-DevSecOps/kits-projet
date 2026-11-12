# OWASP Juice Shop — démarrage

Dépôt d'origine : https://github.com/juice-shop/juice-shop

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/juice-shop/juice-shop.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de OWASP Juice Shop" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
docker build -t app . && docker run -d -p 3000:3000 app
```

Puis ouvrez le port 3000 (onglet Ports) : http://localhost:3000

**À savoir :** la construction prend environ 3 min. Le dépôt ne contient pas de `package-lock.json` : `trivy fs` ne trouve donc aucune dépendance. Générez d'abord le fichier (`npm install --package-lock-only`) ou utilisez `npm audit`. Gitleaks trouve beaucoup de résultats (75), en grande partie des secrets factices volontaires : bon exercice de tri.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
