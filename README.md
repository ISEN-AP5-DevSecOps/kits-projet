# Kits de démarrage du projet DevSecOps AP5

Un dossier par application proposée. Chaque kit contient :

- `.devcontainer/devcontainer.json` : Codespace avec Docker, Node, Java, Python, Ruby et PHP (image universelle de GitHub) ;
- `.github/workflows/ci.yml` : pipeline de base qui construit et démarre l'application (jalon S3) ;
- `DEMARRAGE.md` : import dans le dépôt du groupe, commande de lancement, points d'attention.

| Application | Kit |
|---|---|
| OWASP Juice Shop (Node.js) | [juice-shop](juice-shop/DEMARRAGE.md) |
| OWASP NodeGoat (Node.js, MongoDB) | [nodegoat](nodegoat/DEMARRAGE.md) |
| PyGoat (Python, Django) | [pygoat](pygoat/DEMARRAGE.md) |
| OWASP WebGoat (Java, Spring Boot) | [webgoat](webgoat/DEMARRAGE.md) |
| RailsGoat (Ruby on Rails) | [railsgoat](railsgoat/DEMARRAGE.md) |
| DVWA (PHP, MySQL) | [dvwa](dvwa/DEMARRAGE.md) |

## Mode d'emploi

1. Ouvrez un Codespace sur le dépôt de votre groupe (`projet-groupe-N` → Code → Codespaces → Create).
2. Suivez la section « Importer l'application » du `DEMARRAGE.md` de votre application (une seule personne du groupe).
3. Les autres membres font ensuite `git pull` (ou créent leur propre Codespace).

Les commandes ont été testées dans un runner GitHub Actions. Le pipeline de base n'est qu'un point de départ :
à vous d'y ajouter les briques de sécurité au fil des séances.
