# OWASP Juice Shop — démarrage

Dépôt d'origine : https://github.com/juice-shop/juice-shop

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/juice-shop/juice-shop.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/juice-shop/.devcontainer /tmp/kits/juice-shop/.github .
git add . && git commit -m "Import de OWASP Juice Shop + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
docker build -t app . && docker run -d -p 3000:3000 app
```

Puis ouvrez le port 3000 (onglet Ports) : http://localhost:3000

**À savoir :** la construction prend environ 3 min. Le dépôt ne contient pas de `package-lock.json` : `trivy fs` ne trouve donc aucune dépendance. Générez d'abord le fichier (`npm install --package-lock-only`) ou utilisez `npm audit`. Gitleaks trouve beaucoup de résultats (75), en grande partie des secrets factices volontaires : bon exercice de tri.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
