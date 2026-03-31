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

## 5. Comment Hugo parcourt les fichiers et génère les pages

Quand on lance `hugo` ou `hugo server`, Hugo suit un processus en plusieurs étapes pour transformer les fichiers sources en pages HTML.

### 5.1 Lecture du contenu (`content/`)

Hugo parcourt récursivement le dossier `content/` et lit chaque fichier Markdown (`.md`). Pour chaque fichier, il extrait :

1. Le **front matter** (entre `+++` ou `---`) → les métadonnées de la page (titre, date, paramètres personnalisés…)
2. Le **corps** du fichier → le contenu Markdown, qui sera converti en HTML

```
content/
├── _index.md          → page d'accueil de la section
├── 8_cours_hugo.md    → une page "type : page"
└── posts/
    └── article1.md    → une page "type : posts"
```

### 5.2 Détermination du type et du layout

Pour chaque page, Hugo détermine quel template utiliser selon une **hiérarchie de recherche** (_lookup order_) :

1. Il regarde le champ `type` dans le front matter (ex. `type = "page"`)
2. Sinon, il déduit le type depuis le **nom du dossier parent** dans `content/`
3. Il cherche ensuite le template dans cet ordre :
   - `layouts/<type>/single.html` → template spécifique au type
   - `layouts/_default/single.html` → template générique de fallback
   - Le template du thème en dernier recours

**Exemple pour ce site :**

```
content/8_cours_hugo.md  →  type "page" (par défaut pour la racine)
                         →  layouts/page/single.html  ✓
```

### 5.2.1 Le lien est implicite — aucune déclaration dans les fichiers

C'est un point souvent déroutant pour les débutants : **nulle part** dans `exemple_template.md` on ne dit "utilise `single.html`", et **nulle part** dans `single.html` on ne dit "s'applique aux fichiers de `content/`". Le lien est fait **automatiquement par Hugo** selon deux règles :

**Règle 1 — le type est déduit de la position du fichier**

```
content/
├── exemple_template.md   → à la racine → type = "page"  (automatique)
└── posts/
    └── article.md        → dans posts/ → type = "posts" (automatique)
```

**Règle 2 — Hugo cherche le template selon ce type**

```
type "page"  →  layouts/page/single.html        ← 1er cherché → TROUVÉ ✓
             →  layouts/_default/single.html    ← fallback si absent
             →  themes/ananke/layouts/...       ← fallback thème
```

Pour forcer un type différent, on peut l'écrire explicitement dans le front matter :

```toml
+++
title = "Exemple"
type = "montype"   ← Hugo cherchera alors layouts/montype/single.html
+++
```

### 5.3 Injection des données dans le template

Une fois le template trouvé, Hugo **fusionne** les données de la page avec le template. Il remplace chaque expression `{{ .Variable }}` par sa valeur réelle :

```
front matter              template                    page HTML générée
─────────────             ────────────────────        ─────────────────
title = "Hugo"    →  <h1>{{ .Title }}</h1>   →   <h1>Hugo</h1>
```

C'est ce qu'on appelle le **rendu** (_rendering_).

### 5.4 Génération des URLs

Hugo calcule automatiquement l'URL de chaque page :

- `content/8_cours_hugo.md` → `/8_cours_hugo/` (URL par défaut)
- Si le front matter contient `url = "/hugo"` → l'URL devient `/hugo`

### 5.5 Résultat : le dossier `public/`

Une fois toutes les pages traitées, Hugo écrit les fichiers HTML générés dans `public/`. Ce dossier contient le site complet, prêt à être déployé.

```
public/
├── index.html
├── hugo/
│   └── index.html   ← la page générée depuis 8_cours_hugo.md
└── exemple-template/
    └── index.html   ← la page générée depuis exemple_template.md
```

> **Résumé du pipeline Hugo :**
> `content/*.md` → lecture front matter + corps → choix du template → injection des données → `public/*.html`

---

## 6. Système de Templates

Hugo utilise un système de templates basé sur le langage **Go template**. Un template est un fichier HTML dans lequel on insère des instructions Hugo entre doubles accolades `{{ }}`.

> Lien pour approfondir : https://reintech.io/blog/control-structures-functions-go-tutorial

---

### 5.1 Le contexte `.` (le point)

Dans un template Hugo, **le point `.` représente les données de la page courante**. C'est l'objet auquel vous accédez pour récupérer le titre, la date, le contenu, etc.

---

### 5.2 Variables de la page

Ces variables sont définies dans le **front matter** du fichier Markdown ou fournies par Hugo :

| Variable | Description |
|---|---|
| `{{ .Title }}` | Titre de la page |
| `{{ .Date }}` | Date de publication |
| `{{ .Content }}` | Contenu Markdown converti en HTML |
| `{{ .Description }}` | Description (champ `description` du front matter) |
| `{{ .Params.auteur }}` | Paramètre personnalisé `auteur` du front matter |
| `{{ .Site.Title }}` | Titre global du site (depuis `config.toml`) |

**Exemple de front matter** dans un fichier Markdown :

```toml
+++
title = "Mon cours"
date = "2025-03-01"
description = "Introduction aux templates Hugo"
[params]
  auteur = "Alice"
  niveau = "débutant"
+++
```

**Template correspondant** (`layouts/page/single.html`) :

```html
<h1>{{ .Title }}</h1>
<p>Par {{ .Params.auteur }} — niveau : {{ .Params.niveau }}</p>
<p><em>{{ .Description }}</em></p>
{{ .Content }}
```

---

### 5.3 Conditions avec `if`

On peut afficher ou masquer du contenu selon une condition :

```html
{{ if .Params.auteur }}
  <p>Auteur : {{ .Params.auteur }}</p>
{{ else }}
  <p>Auteur inconnu</p>
{{ end }}
```

> La condition est vraie si la variable existe et n'est pas vide.

---

### 5.4 Boucles avec `range`

`range` permet d'itérer sur une liste. Exemple : afficher tous les articles du site :

```html
<ul>
  {{ range .Site.Pages }}
    <li><a href="{{ .Permalink }}">{{ .Title }}</a></li>
  {{ end }}
</ul>
```

On peut aussi itérer sur une liste définie dans le front matter :

```toml
+++
title = "Cours Hugo"
[params]
  competences = ["HTML", "CSS", "Markdown"]
+++
```

```html
<ul>
  {{ range .Params.competences }}
    <li>{{ . }}</li>
  {{ end }}
</ul>
```

> Dans la boucle, le point `.` représente l'élément courant de la liste.

---

### 5.5 Partials — réutiliser des morceaux de template

Un **partial** est un fragment de template réutilisable, stocké dans `layouts/partials/`.

**Appel dans un template :**

```html
{{ partial "entete.html" . }}
```

> Le second argument `.` transmet le contexte (les données de la page) au partial.

**Contenu de `layouts/partials/entete.html` :**

```html
<header>
  <h1>{{ .Title }}</h1>
  {{ if .Date }}
    <p>Publié le {{ .Date.Format "02/01/2006" }}</p>
  {{ end }}
</header>
```

---

### 5.6 Héritage avec `baseof.html`, `block` et `define`

Hugo permet de définir une **mise en page de base** dans `layouts/_default/baseof.html`, avec des zones à remplir :

```html
<!DOCTYPE html>
<html>
  <head><title>{{ .Title }}</title></head>
  <body>
    {{ block "main" . }}{{ end }}
  </body>
</html>
```

Chaque template enfant remplit ces zones avec `define` :

```html
{{ define "main" }}
  <h1>{{ .Title }}</h1>
  {{ .Content }}
{{ end }}
```

C'est exactement le fonctionnement du template de ce site : `layouts/page/single.html` définit le bloc `"main"` qui est injecté dans la mise en page du thème Ananke.

---

### 5.7 Exemple complet — template de ce site

Voici le template réel utilisé pour les pages de cours (`layouts/page/single.html`) :

```html
{{ define "header" }}{{ partial "page-header.html" . }}{{ end }}
{{ define "main" }}
  <div class="flex-l mt2 mw9 center">
    <article class="center cf pv5 mw9">
      <header>
        <h1 class="f1">{{ .Title }}</h1>
      </header>
      <div class="nested-copy-line-height lh-copy f4 nested-links mid-gray">
        {{ .Content }}
      </div>
    </article>
  </div>
{{ end }}
```

Il utilise :
- `define "main"` pour s'insérer dans la mise en page du thème
- `partial "page-header.html" .` pour l'en-tête réutilisable
- `.Title` et `.Content` pour les données de la page

> **Exercice** : Observez la page [Exemple de template](/exemple-template) de ce site. Repérez comment les variables du front matter apparaissent dans la page rendue.

---

## 7. Commandes Hugo utiles

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

## 8. Thèmes Hugo

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

## 9. Ressources supplémentaires

### Les tutos

- [Documentation officielle Hugo](https://gohugo.io/documentation/)
- [Tutoriel bien 1](https://bout2code.fr/tutos/creer-un-site-avec-hugo/)
- [Tutoriel bien 2](https://kinsta.com/fr/blog/hugo-site-statique/)
- [Tutoriel rapide Hugo](https://www.w3schools.com/whatis/whatis_hugo.asp)

### Les thèmes

- [Thèmes officielles Hugo](https://themes.gohugo.io/)
- [Pré-sélection de thèmes](https://cloudcannon.com/blog/fifty-of-the-most-popular-hugo-themes/)
