+++
title='Hugo sur GitHub Pages'
url="hugogithubpages"
+++

# Hugo sur GitHub Pages

Ce guide vous explique comment héberger votre site Hugo sur GitHub Pages en utilisant **GitHub Actions** pour une intégration et un déploiement continus.

## Types de sites sur GitHub Pages

GitHub Pages propose trois types de sites :

- **Sites de projet** : Associés à un projet spécifique hébergé sur GitHub.
- **Sites utilisateur** : Associés à un compte GitHub personnel.
- **Sites d'organisation** : Associés à une organisation sur GitHub.

Pour comprendre les exigences en matière de propriété et de nommage des dépôts, consultez la [documentation de GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites).

## Configuration de GitHub Pages

1. Accédez à votre dépôt sur GitHub.
2. Cliquez sur l'onglet **"Settings"** (Paramètres).
3. Dans le menu latéral, sélectionnez **"Pages"**.
4. Sous la section **"Build and deployment"**, assurez-vous que la source est définie sur **"GitHub Actions"**.

## Configuration de GitHub Actions pour le déploiement

1. Dans votre projet local, créez le répertoire `.github/workflows` :

   ```bash
   mkdir -p .github/workflows
   ```

2. Créez un fichier nommé `hugo.yaml` dans ce répertoire :

   ```bash
   touch .github/workflows/hugo.yaml
   ```

3. Ouvrez ce fichier et ajoutez-y le contenu suivant :

   ```yaml
   # Workflow pour construire et déployer un site Hugo sur GitHub Pages
   name: Déployer le site Hugo sur Pages

   on:
     push:
       branches:
         - main

     workflow_dispatch:

   permissions:
     contents: read
     pages: write
     id-token: write

   concurrency:
     group: "pages"
     cancel-in-progress: false

   jobs:
     build:
       runs-on: ubuntu-latest
       env:
         HUGO_VERSION: 0.144.2
       steps:
         - name: Installer Hugo CLI
           run: |
             wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
             && sudo dpkg -i ${{ runner.temp }}/hugo.deb
         - name: Installer Dart Sass
           run: sudo snap install dart-sass
         - name: Checkout du dépôt
           uses: actions/checkout@v4
           with:
             submodules: recursive
             fetch-depth: 0
         - name: Configurer Pages
           id: pages
           uses: actions/configure-pages@v5
         - name: Installer les dépendances Node.js
           run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
         - name: Construire le site avec Hugo
           env:
             HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
             HUGO_ENVIRONMENT: production
             TZ: America/Los_Angeles
           run: |
             hugo \
               --gc \
               --minify \
               --baseURL "${{ steps.pages.outputs.base_url }}/"
         - name: Télécharger l'artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: ./public

     deploy:
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       runs-on: ubuntu-latest
       needs: build
       steps:
         - name: Déployer sur GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v4
   ```

   > **Remarque** : Adaptez la version de Hugo (`HUGO_VERSION`) selon vos besoins.

## Pousser les modifications et déployer

1. Ajoutez le fichier de workflow au suivi Git et poussez les modifications :

   ```bash
   git add .github/workflows/hugo.yaml
   git commit -m "Ajouter le workflow de déploiement Hugo"
   git push
   ```

2. Accédez à l'onglet **"Actions"** de votre dépôt GitHub pour suivre l'exécution du workflow.

3. Une fois le workflow terminé avec succès, votre site sera disponible à l'adresse `https://votre-utilisateur.github.io/mon-site-hugo/`.

---

Pour plus de détails et de ressources supplémentaires, consultez la documentation officielle de Hugo sur le déploiement sur GitHub Pages : [https://gohugo.io/host-and-deploy/host-on-github-pages/](https://gohugo.io/host-and-deploy/host-on-github-pages/).
