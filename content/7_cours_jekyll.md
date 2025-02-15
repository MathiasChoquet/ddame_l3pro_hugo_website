+++
title='Jekyll'
url = "/jekyll"
+++

# Jekyll : Présentation et Fonctionnalités

Jekyll est un générateur de site statique (_Static Site Generator_) écrit en Ruby. Il est particulièrement adapté aux blogs, portfolios et sites de documentation. Grâce à son intégration avec GitHub Pages, il permet de déployer facilement un site sans serveur ni base de données.

---

## 1. Qu'est-ce que Jekyll ?

Jekyll transforme des fichiers écrits en **Markdown**, **HTML**, et **Liquid** en un site web statique. Il prend un ensemble de fichiers et les compile pour générer un site web rapide et léger.

### Pourquoi utiliser Jekyll ?

- **Pas de base de données** : Uniquement des fichiers statiques = rapidité et sécurité.
- **Flexibilité** : Utilisation de templates personnalisés avec Liquid.
- **Intégration GitHub Pages** : Déploiement gratuit et automatique.
- **Support Markdown** : Facilité d'écriture des articles et pages.

---

## 2. Structure d'un projet Jekyll

Un projet Jekyll est organisé de cette manière :

```
mon-site-jekyll/
├── _config.yml      # Configuration du site
├── _layouts/        # Templates HTML
├── _includes/       # Fragments de page réutilisables
├── _posts/          # Articles de blog (YYYY-MM-DD-titre.md)
├── _site/           # Site généré (ne pas modifier)
├── assets/          # Fichiers CSS, JS, images
├── index.md         # Page d'accueil
```

### Rôles des principaux fichiers et dossiers

- **`_config.yml`** : Contient la configuration globale du site.
- **`_layouts/`** : Contient les modèles de page pour structurer le site.
- **`_posts/`** : Contient les articles de blog avec un format de date spécifique.
- **`_site/`** : Dossier généré après la compilation (ne pas modifier directement).

---

## 3. Fonctionnement de Jekyll

### 3.1 Installation de Jekyll

Avant d'utiliser Jekyll, installez Ruby et Jekyll avec la commande :

```bash
gem install jekyll bundler
```

### 3.2 Création d'un projet Jekyll

Pour créer un nouveau site Jekyll :

```bash
jekyll new mon-site
cd mon-site
```

### 3.3 Lancer un serveur local

```bash
bundle exec jekyll serve
```

Le site est accessible à `http://localhost:4000`.

### 3.4 Génération des fichiers statiques

```bash
jekyll build
```

Les fichiers générés se trouvent dans le dossier `_site/`.

---

## 4. Surcharge des fichiers de template

Jekyll permet de modifier les fichiers du thème utilisé en les copiant dans le répertoire local.

### Exemple de surcharge :

Si vous utilisez le thème **Minima** et souhaitez modifier la page d'accueil, suivez ces étapes :

1. Copiez le fichier de layout du thème :
   ```bash
   cp /path/to/minima/_layouts/home.html ./_layouts/home.html
   ```
2. Modifiez le fichier copié selon vos besoins.
3. Jekyll utilisera la version locale du fichier au lieu de celui du thème.

---

## 5. Configuration dans `_config.yml`

Le fichier `_config.yml` permet de configurer différents aspects du site.

Exemple :

```yaml
title: "Mon Blog Jekyll"
author: "Jean Dupont"
email: "jean@example.com"
baseurl: ""
url: "https://monsite.com"
```

### Paramètres utiles :

- **`baseurl`** : Spécifie un sous-répertoire si nécessaire.
- **`permalink`** : Définit le format des URLs des articles.
- **`theme`** : Indique le thème utilisé.

---

## 6. Articles et Pages

Jekyll gère les articles via le dossier `_posts/` et les pages via des fichiers `.md` dans la racine du projet.

### Exemple d'article dans `_posts/` :

```markdown
---
title: "Mon premier article"
date: 2025-01-01
tags: [blog, tuto]
---

# Bienvenue sur mon blog !

Voici mon premier article avec Jekyll.
```

### Exemple de page :

```markdown
---
title: "À propos"
layout: page
permalink: /about/
---

# Qui suis-je ?

Je suis un passionné de développement web.
```

---

## 7. Déploiement sur GitHub Pages

Jekyll est compatible avec **GitHub Pages**, ce qui permet de publier facilement un site.

### Étapes :

1. Créez un dépôt GitHub avec le nom `mon-site.github.io`.
2. Ajoutez votre projet Jekyll et poussez-le sur GitHub :
   ```bash
   git init
   git add .
   git commit -m "Premier commit"
   git branch -M main
   git remote add origin https://github.com/utilisateur/mon-site.github.io.git
   git push -u origin main
   ```
3. Activez GitHub Pages dans les paramètres du dépôt.

Votre site sera accessible à `https://utilisateur.github.io/`.

---

## 8. Ressources supplémentaires

- [Documentation officielle de Jekyll](https://jekyllrb.com/docs/)
- [Thèmes Jekyll](https://github.com/topics/jekyll-theme)
- [Tutoriel W3Schools sur Jekyll](https://www.w3schools.com/whatis/whatis_jekyll.asp)

---
