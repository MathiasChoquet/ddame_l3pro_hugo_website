+++
title='CSS'
url="css"
+++

# Introduction

## Qu'est-ce que le CSS ?

CSS (_Cascading Style Sheets_) est un langage qui décrit le style visuel des pages web. Il permet de styliser la page (couleurs, tailles, dispositions, etc.).

---

# Partie 1 : CSS - Introduction et concepts de base

## Selectors (simples et complexes)

- **Selector simple** : `h1 { color: red; }`
- **Selector complexe** : `.menu a:hover { color: blue; }`

## Propriétés CSS essentielles

1. **Couleur** :
   ```css
   p {
     color: blue;
     background-color: lightgrey;
   }
   ```
2. **Texte et polices** :
   ```css
   h1 {
     font-family: Arial, sans-serif;
     font-size: 24px;
   }
   ```
3. **Espacement** :
   ```css
   div {
     margin: 10px;
     padding: 5px;
   }
   ```
4. **Bordures** :
   ```css
   div {
     border: 2px solid black;
   }
   ```

## Types d'insertion

1. **CSS en ligne** :
   ```html
   <p style="color: red;">Texte rouge</p>
   ```
2. **CSS interne** :
   ```html
   <style>
     body {
       background-color: lightblue;
     }
   </style>
   ```
3. **CSS externe** :
   ```html
   <link rel="stylesheet" href="styles.css" />
   ```

---

# Partie 2 : CSS avancé

## Flexbox

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

## Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

## Les pseudo-classes et pseudo-éléments

```css
button:hover {
  background-color: green;
}

p::before {
  content: "Note : ";
}
```

## Animations CSS

```css
@keyframes example {
  from {
    background-color: red;
  }
  to {
    background-color: yellow;
  }
}

div {
  animation: example 3s infinite;
}
```

## Media Queries

```css
@media (max-width: 600px) {
  body {
    background-color: lightgrey;
  }
}
```

---

# Exercices pratiques

## Exercice 1 : Styliser une page HTML

- Ajouter des couleurs et polices à une page HTML existante.

## Exercice 2 : Construire une mise en page responsive

- Utiliser Grid pour créer un layout.
