+++
title = "Exemple de template HUGO"
url = "/exemple-template"
date = "2025-03-01"
description = "Cette page illustre le lien entre le front matter d'un fichier Markdown et le template Hugo qui l'affiche."

[params]
  competences = ["HTML", "CSS", "Hugo", "Template"]
+++

## À quoi sert cette page ?

Cette page est un **exemple pédagogique** destiné à illustrer le cours sur les templates Hugo.

Elle est rendue par le template `layouts/page/single.html` du site, qui utilise `{{ define "main" }}` pour s'injecter dans la mise en page du thème Ananke.

---

## Ce que contient le front matter de cette page

Voici les variables définies dans l'en-tête (front matter) de ce fichier Markdown :

```toml
title = "Exemple de template"
date = "2025-03-01"
description = "Cette page illustre le lien entre le front matter..."

[params]
  auteur = "Mathias CHOQUET"
  niveau = "débutant"
  competences = ["HTML", "CSS", "Hugo","template"]
```

---

## Comment un template accède à ces données

Dans un template Hugo, on écrit :

| Expression dans le template       | Valeur affichée        |
| --------------------------------- | ---------------------- |
| `{{ .Title }}`                    | Exemple de template    |
| `{{ .Date.Format "02/01/2006" }}` | 01/03/2025             |
| `{{ .Description }}`              | Cette page illustre... |
| `{{ .Params.auteur }}`            | Alice Dupont           |
| `{{ .Params.niveau }}`            | débutant               |

Et pour la liste `competences`, on utilise `range` :

```html
{{ range .Params.competences }}
<li>{{ . }}</li>
{{ end }}
```

Ce qui produira :

- HTML
- CSS
- Hugo

---
