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
   # Sample workflow for building and deploying a Hugo site to GitHub Pages
   name: Deploy Hugo site to Pages

   on:
     # Runs on pushes targeting the default branch
     push:
       branches: ["main"]

     # Allows you to run this workflow manually from the Actions tab
     workflow_dispatch:

   # Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
   permissions:
     contents: read
     pages: write
     id-token: write

   # Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
   # However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
   concurrency:
     group: "pages"
     cancel-in-progress: false

   # Default to bash
   defaults:
     run:
       shell: bash

   jobs:
     # Build job
     build:
       runs-on: ubuntu-latest # Use the latest Ubuntu runner
       env:
         HUGO_VERSION: 0.128.0 # Define the Hugo version to install
       steps:
         # Download and install the specified Hugo version
         - name: Install Hugo CLI
           run: |
             wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
             && sudo dpkg -i ${{ runner.temp }}/hugo.deb
         - name: Install Dart Sass
           run: sudo snap install dart-sass
         - name: Checkout
           uses: actions/checkout@v4
           with:
             submodules: recursive # Ensure submodules are checked out
         - name: Setup Pages
           id: pages
           uses: actions/configure-pages@v5 # Setup GitHub Pages configuration for deployment
         - name: Install Node.js dependencies # install npm dependencies if needed
           run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
         - name: Build with Hugo
           env:
             HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache # use a temporary cache
             HUGO_ENVIRONMENT: production # build with the hugo command
           run: |
             hugo \
               --minify \
               --baseURL "${{ steps.pages.outputs.base_url }}/"
         - name: Upload artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: ./public # Upload the generated site for deployment (store it to deploy step)

     # Deployment job
     deploy:
       environment:
         name: github-pages # Define the GitHub Pages environment
         url: ${{ steps.deployment.outputs.page_url }}
       runs-on: ubuntu-latest # Use the latest Ubuntu runner
       needs: build # Ensure build completes before deploying
       steps:
         - name: Deploy to GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v4
           # Deploy the generated site to GitHub Pages
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
