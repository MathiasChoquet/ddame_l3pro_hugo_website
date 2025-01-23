+++
title='Hugo'
url="hugo"
+++

# Guide d'utilisation de Hugo

Hugo est un générateur de site statique (_Static Site Generator_) performant et flexible, écrit en Go. Il est connu pour sa rapidité et sa capacité à gérer des sites volumineux.

---

## 1. Introduction à Hugo

### Pourquoi utiliser Hugo ?

1. **Rapidité** : Hugo est capable de générer des milliers de pages en quelques secondes.
2. **Simplicité** : Hugo utilise des fichiers Markdown et une structure simple pour organiser le contenu.
3. **Flexibilité** : Une grande variété de thèmes et un système de templates puissant.

### Cas d'utilisation

- Blogs
- Documentation
- Portfolios
- Sites web institutionnels

---

## 2. Structure d'un projet Hugo

Voici la structure typique d'un projet Hugo :

```
mon-site/
├── archetypes/       # Modèles pour créer de nouveaux contenus
├── content/          # Contenus du site (articles, pages)
├── data/             # Fichiers de données (JSON, YAML, TOML)
├── layouts/          # Templates personnalisés
├── static/           # Fichiers statiques (images, CSS, JS)
├── themes/           # Thèmes pour le site
├── config.toml       # Fichier de configuration
```

### Rôle des principaux dossiers :

- ``: Contient les fichiers Markdown organisés par type (ex. :`content/blog/`, `content/docs/`).
- `` : Contient les templates pour structurer les pages.
- `` : Contient les fichiers statiques accessibles directement (images, CSS).
- `` : Contient les thèmes installés.

---

## 3. Configuration de Hugo

La configuration de Hugo est généralement définie dans un fichier `config.toml`. Voici un exemple basique :

```toml
title = "Mon site Hugo"
baseURL = "https://monsite.com"
theme = "mon-theme"
languageCode = "fr"
enableRobotsTXT = true
```

### Options utiles :

- `` : L'URL de base du site (nécessaire pour les liens).
- `` : Le thème à utiliser.
- `` : Langue du site.
- ``: Génère un fichier`robots.txt` pour le référencement.

---

## 4. Créer et gérer du contenu

### Créer une nouvelle page

Pour créer un nouvel article ou une page :

```bash
hugo new blog/mon-article.md
```

Cela crée un fichier Markdown dans `content/blog/` avec un front matter pré-rempli :

```markdown
---
title= "Mon article"
date: 2025-01-01
description: "Description de l'article."
draft: true
---
```

### Modifier un contenu

Modifiez le fichier Markdown créé pour ajouter du contenu. Exemple :

```markdown
# Mon article

Bienvenue dans mon premier article écrit avec Hugo !
```

---

## 5. Système de Templates

Hugo utilise un système de templates puissant pour personnaliser l'apparence des pages.

### Exemple de template pour une page d'article

Créez un fichier `layouts/_default/single.html` :

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Title }}</title>
  </head>
  <body>
    <header>
      <h1>{{ .Title }}</h1>
      <p>{{ .Date }}</p>
    </header>
    <main>{{ .Content }}</main>
  </body>
</html>
```

### Variables Hugo utiles

- `{{ .Title }}` : Le titre de la page.
- `{{ .Date }}` : La date de publication.
- `{{ .Content }}` : Le contenu principal de la page.

---

## 6. Commandes Hugo utiles

1. **Créer un nouveau site Hugo** :

   ```bash
   hugo new site mon-site
   ```

2. **Ajouter un contenu** :

   ```bash
   hugo new blog/mon-article.md
   ```

3. **Lancer un serveur local** :

   ```bash
   hugo server
   ```

   Accédez au site à `http://localhost:1313`.

4. **Construire le site** :

   ```bash
   hugo
   ```

   Les fichiers sont générés dans le dossier `public/`.

---

## 7. Thèmes Hugo

Hugo propose une large bibliothèque de thèmes disponibles sur [themes.gohugo.io](https://themes.gohugo.io/).

### Installer un thème

1. Ajoutez le thème en tant que sous-module Git :
   ```bash
   git submodule add https://github.com/thematique/hugo-theme-mon-theme.git themes/mon-theme
   ```
2. Activez le thème dans `config.toml` :

   ```toml

   ```

theme = "mon-theme"

```

---

## 8. Ressources supplémentaires

- [Documentation officielle Hugo](https://gohugo.io/documentation/)
- [Thèmes Hugo](https://themes.gohugo.io/)
- [Tutoriel rapide Hugo](https://www.w3schools.com/whatis/whatis_hugo.asp)

```
