+++
title='HTML'
url = "/html"
+++

# Introduction

## Qu'est-ce que le HTML ?

HTML (_HyperText Markup Language_) est un langage qui structure le contenu des pages web. Il permet de définir la structure (titres, paragraphes, images, etc.).

## Leur importance dans le monde numérique

1. **Accessibilité** : HTML permet de rendre les contenus accessibles sur différents appareils.
2. **Base de tous les sites web** : Ces technologies sont à la base de tous les sites web modernes.

---

# Partie 1 : HTML - Structure de base

## Comprendre les balises, attributs, et structure d'une page

Une page HTML se compose de **balises**, qui définissent la structure, et d'attributs, qui ajoutent des informations aux balises.

## Exemple : Structure de base

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Exemple de page</title>
  </head>
  <body>
    <h1>Bienvenue</h1>
    <p>Ceci est une introduction à HTML.</p>
  </body>
</html>
```

## Types de balises

1. **Structurelles** : `<html>`, `<head>`, `<body>`
2. **Texte** : `<h1>` à `<h6>` pour les titres, `<p>` pour les paragraphes.
3. **Liens** : `<a href="https://example.com">Lien</a>`.
4. **Images** : `<img src="image.png" alt="Description">`.

## Les commentaires et leur utilité

```html
<!-- Ceci est un commentaire HTML -->
```

---

# Partie 2 : HTML avancé

## Listes (ordonnées et non ordonnées)

```html
<h3>Liste non ordonnée</h3>
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<h3>Liste ordonnée</h3>
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
</ol>
```

## Tableaux et leur structure

```html
<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Jean</td>
      <td>25</td>
    </tr>
    <tr>
      <td>Marie</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
```

## Formulaires

```html
<form action="/submit" method="post">
  <label for="nom">Nom :</label>
  <input type="text" id="nom" name="nom" />
  <button type="submit">Envoyer</button>
</form>
```

## Sémantique HTML

Les balises sémantiques permettent de mieux structurer le contenu pour les utilisateurs et les moteurs de recherche.

```html
<header>
  <h1>Mon Site</h1>
</header>
<main>
  <article>
    <h2>Article 1</h2>
    <p>Contenu de l'article.</p>
  </article>
</main>
<footer>
  <p>&copy; 2025</p>
</footer>
```

---

# Exercices pratiques

## Exercice 1 : Créer une page de présentation

- Inclure un `<header>`, `<main>` et `<footer>`.

## Exercice 2 : Construire une page produit

- Inclure une image, un titre et un bouton dans un `<div>`.

# Ressources supplémentaires

- [Liste des balises](https://developer.mozilla.org/fr/docs/Web/HTML/Element)
- [Validateur W3C](https://validator.w3.org/)

---
