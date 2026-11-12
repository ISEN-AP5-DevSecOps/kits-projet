# OWASP WebGoat — démarrage

Dépôt d'origine : https://github.com/WebGoat/WebGoat

## Importer l'application dans votre dépôt de groupe (une seule personne)

Dans un Codespace ouvert sur votre dépôt `projet-groupe-N` :

```bash
git clone --depth 1 https://github.com/WebGoat/WebGoat.git /tmp/app
rm -rf /tmp/app/.git /tmp/app/.github
cp -r /tmp/app/. .
git add . && git commit -m "Import de OWASP WebGoat" && git push
```

Copiez ensuite le dossier `.devcontainer` et `.github/workflows/ci.yml` de ce kit dans votre dépôt,
puis recréez le Codespace (Codespaces: Rebuild Container).

## Lancer l'application dans le Codespace

```bash
./mvnw -B -q clean install -DskipTests && docker build -t app . && docker run -d -p 8080:8080 app
```

Puis ouvrez le port 8080 (onglet Ports) : http://localhost:8080/WebGoat

**À savoir :** WebGoat exige Java 25 (installé par le pipeline). Dans le Codespace, si Java 25 manque, explorez l'application avec l'image officielle : `docker run -d -p 8080:8080 webgoat/webgoat`. Pour la SCA Java, OWASP Dependency-Check est plus précis que Trivy.

Testé le 12/11/2026 dans un runner GitHub Actions : démarrage OK, Gitleaks, Semgrep, Trivy, Hadolint et ZAP baseline fonctionnent.
