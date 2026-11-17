# OWASP WebGoat — démarrage

Dépôt d'origine : https://github.com/WebGoat/WebGoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/WebGoat/WebGoat.git /tmp/app
git clone --depth 1 https://github.com/ISEN-AP5-DevSecOps/kits-projet.git /tmp/kits
rm -rf /tmp/app/.git /tmp/app/.github
mv README.md PROJET.md                 # garde les consignes du projet (le README de l'application va le remplacer)
cp -r /tmp/app/. .
cp -r /tmp/kits/webgoat/.devcontainer /tmp/kits/webgoat/.github .
git add . && git commit -m "Import de OWASP WebGoat + kit de démarrage" && git push
```

Puis recréez le Codespace pour qu'il prenne la configuration du kit :
Ctrl+Shift+P → **Codespaces: Rebuild Container**.

Le pipeline de base (onglet Actions) doit passer au vert après le push.

## Lancer l'application dans le Codespace

```bash
chmod +x mvnw && ./mvnw -B -q clean install -DskipTests && docker build -t app . && docker run -d -p 8080:8080 app
```

Puis ouvrez le port 8080 (onglet Ports) : http://localhost:8080/WebGoat

**À savoir :** WebGoat exige Java 25 (installé par le pipeline). Dans le Codespace, si Java 25 manque, explorez l'application avec l'image officielle : `docker run -d -p 8080:8080 webgoat/webgoat`. Pour la SCA Java, OWASP Dependency-Check est plus précis que Trivy.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
