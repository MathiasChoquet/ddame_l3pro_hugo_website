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

# Partie 3 : CSS Utilitaire — Tachyons

## Petit historique des frameworks CSS

Les frameworks CSS sont apparus pour résoudre un problème récurrent : écrire du CSS cohérent, maintenable et compatible entre navigateurs est fastidieux. Trois grandes approches se sont succédé.

### Bootstrap (2011) — l'approche par composants

Créé par Twitter, **Bootstrap** est le framework CSS le plus utilisé au monde. Son principe : fournir des **composants prêts à l'emploi** (boutons, formulaires, grilles, modales, etc.) que l'on active via des classes prédéfinies.

```html
<!-- Bootstrap : une classe = un composant entier -->
<button class="btn btn-primary btn-lg">Envoyer</button>
<div class="alert alert-danger">Erreur !</div>
<div class="row">
  <div class="col-md-6">Colonne gauche</div>
  <div class="col-md-6">Colonne droite</div>
</div>
```

**Avantages :** très rapide à mettre en œuvre, documentation abondante, composants interactifs (via JavaScript).

**Limites :** les sites "ont tous l'air Bootstrap", personnaliser en profondeur est difficile, le fichier CSS est lourd (~160 Ko minifié).

---

### Tachyons (2014) — l'approche utilitaire

**Tachyons** a introduit une idée radicalement différente : plutôt que des composants, fournir des **classes atomiques** — une classe = une seule propriété CSS. On compose le style directement dans le HTML.

```html
<!-- Tachyons : on combine des classes atomiques -->
<button class="ph4 pv2 bg-blue white br2 fw6 f5 pointer">Envoyer</button>
```

Chaque classe fait une seule chose : `ph4` = padding horizontal, `bg-blue` = fond bleu, `br2` = coins arrondis, etc.

---

### Tailwind CSS (2017) — l'approche utilitaire moderne

**Tailwind CSS** reprend le principe de Tachyons et l'industrialise : nommage plus lisible, configuration poussée, et surtout un système de **purge automatique** qui supprime les classes non utilisées au build. Le fichier CSS final ne contient que ce dont la page a besoin.

```html
<!-- Tailwind : syntaxe plus explicite -->
<button class="px-4 py-2 bg-blue-500 text-white rounded font-semibold text-sm cursor-pointer">
  Envoyer
</button>
```

Tailwind est aujourd'hui le framework CSS le plus populaire dans les nouveaux projets, notamment avec React, Vue et Next.js.

---

### Comparaison synthétique

| | Bootstrap | Tachyons | Tailwind |
|---|---|---|---|
| Année | 2011 | 2014 | 2017 |
| Approche | Composants | Utilitaire atomique | Utilitaire moderne |
| Taille | ~160 Ko | ~73 Ko | < 10 Ko (purgé) |
| Personnalisation | Limitée | Moyenne | Très élevée |
| Courbe d'apprentissage | Faible | Moyenne | Moyenne |
| Popularité actuelle | Élevée | Faible | Très élevée |

---

## Principe

Le CSS "utilitaire" (ou "atomic CSS") est une approche où l'on n'écrit plus de classes sémantiques dans un fichier `.css`, mais où l'on compose le style directement dans le HTML en combinant de petites classes à usage unique.

**Tachyons** est l'un des frameworks pionniers de cette approche. Chaque classe correspond exactement à **une seule propriété CSS** avec une valeur fixe.

```css
/* CSS classique : on invente un nom, on écrit les règles */
.titre-section {
  font-size: 1.25rem;
  font-weight: 600;
  text-transform: uppercase;
  color: #555;
  margin-bottom: 1rem;
}
```

```html
<!-- Tachyons : les propriétés sont directement dans les classes HTML -->
<h2 class="f4 fw6 ttu mid-gray mb3">Mon titre</h2>
```

## Nomenclature

Les noms de classes suivent des abréviations systématiques. Comprendre le système permet de deviner une classe sans consulter la documentation.

| Catégorie | Préfixe | Propriété CSS |
|---|---|---|
| Taille de texte | `f1` … `f7` | `font-size` (de 3rem à 0.75rem) |
| Graisse | `fw1` … `fw9` | `font-weight` |
| Hauteur de ligne | `lh-` | `line-height` |
| Transformation | `tt` | `text-transform` |
| Espacement lettres | `tracked` | `letter-spacing` |
| Marges | `m`, `mt`, `mr`, `mb`, `ml`, `mv`, `mh`, `ma` | `margin` |
| Paddings | `p`, `pt`, `pr`, `pb`, `pl`, `pv`, `ph`, `pa` | `padding` |
| Largeur | `w-` | `width` |
| Hauteur | `h-` | `height` |
| Affichage | `db`, `di`, `dib`, `dn` | `display` |
| Flexbox | `flex`, `flex-wrap`, `justify-` | `display: flex` + dérivés |
| Couleur texte | nom de couleur | `color` |
| Couleur fond | `bg-` | `background-color` |
| Bordures | `ba`, `bt`, `br`, `bb`, `bl` | `border` |
| Coins arrondis | `br1` … `br4`, `br-pill` | `border-radius` |
| Ombres | `shadow-1` … `shadow-4` | `box-shadow` |
| Opacité | `o-10` … `o-100` | `opacity` |
| Position | `static`, `relative`, `absolute`, `fixed` | `position` |

## Échelle des espacements

Tachyons utilise une échelle de taille cohérente pour les marges et paddings, basée sur des multiples de `rem` :

| Indice | Valeur |
|---|---|
| `0` | `0` |
| `1` | `0.25rem` (~4px) |
| `2` | `0.5rem` (~8px) |
| `3` | `1rem` (~16px) |
| `4` | `2rem` (~32px) |
| `5` | `4rem` (~64px) |
| `6` | `8rem` (~128px) |
| `7` | `16rem` (~256px) |

Les suffixes de direction : `a` = all (toutes directions), `h` = horizontal, `v` = vertical, `t/r/b/l` = top/right/bottom/left.

```css
/* Exemples d'équivalences */
.ma3  → margin: 1rem;
.ph2  → padding-left: 0.5rem; padding-right: 0.5rem;
.mt4  → margin-top: 2rem;
.pb0  → padding-bottom: 0;
```

## Typographie

```html
<!-- Taille (f1 = plus grand, f7 = plus petit) -->
<p class="f1">3rem</p>
<p class="f3">1.5rem</p>
<p class="f6">0.875rem</p>

<!-- Graisse -->
<p class="fw3">Light</p>
<p class="fw6">Semi-bold</p>
<p class="fw9">Black</p>

<!-- Hauteur de ligne -->
<p class="lh-solid">Serré (1)</p>
<p class="lh-copy">Lecture (1.5)</p>
<p class="lh-double">Double (2)</p>

<!-- Transformation et espacement -->
<p class="ttu">TOUT EN MAJUSCULES</p>
<p class="ttl">tout en minuscules</p>
<p class="tracked">l e t t r e s   é c a r t é e s</p>
<p class="tracked-tight">lettres resserrées</p>

<!-- Alignement -->
<p class="tl">Aligné à gauche</p>
<p class="tc">Centré</p>
<p class="tr">Aligné à droite</p>
<p class="tj">Justifié</p>
```

## Couleurs

Tachyons fournit une palette de couleurs nommées, utilisables directement sur le texte ou le fond :

```html
<!-- Couleurs de texte -->
<p class="black">black</p>
<p class="dark-gray">dark-gray</p>
<p class="mid-gray">mid-gray</p>
<p class="gray">gray</p>
<p class="silver">silver</p>
<p class="light-silver">light-silver</p>
<p class="moon-gray">moon-gray</p>
<p class="near-white">near-white</p>

<!-- Couleurs vives -->
<p class="dark-red">dark-red</p>
<p class="red">red</p>
<p class="orange">orange</p>
<p class="gold">gold</p>
<p class="yellow">yellow</p>
<p class="green">green</p>
<p class="navy">navy</p>
<p class="dark-blue">dark-blue</p>
<p class="blue">blue</p>
<p class="purple">purple</p>

<!-- Couleurs de fond : préfixe bg- -->
<div class="bg-light-blue">bg-light-blue</div>
<div class="bg-light-green">bg-light-green</div>
<div class="bg-light-yellow">bg-light-yellow</div>
<div class="bg-light-red">bg-light-red</div>
<div class="bg-near-white">bg-near-white</div>
<div class="bg-black-10">bg-black-10 (noir à 10% opacité)</div>
```

## Mise en page — Flexbox

Tachyons expose les principales propriétés Flexbox via des classes :

```html
<div class="flex flex-wrap justify-between items-center">
  <div class="w-33">Colonne 1</div>
  <div class="w-33">Colonne 2</div>
  <div class="w-33">Colonne 3</div>
</div>
```

| Classe | Équivalent CSS |
|---|---|
| `flex` | `display: flex` |
| `flex-wrap` | `flex-wrap: wrap` |
| `flex-column` | `flex-direction: column` |
| `justify-start` | `justify-content: flex-start` |
| `justify-center` | `justify-content: center` |
| `justify-between` | `justify-content: space-between` |
| `justify-around` | `justify-content: space-around` |
| `items-start` | `align-items: flex-start` |
| `items-center` | `align-items: center` |
| `items-end` | `align-items: flex-end` |

## Bordures et effets

```html
<!-- Bordures -->
<div class="ba">Bordure sur tous les côtés</div>
<div class="bt">Bordure en haut seulement</div>
<div class="b--light-gray">Couleur de bordure gris clair</div>
<div class="bw1">Épaisseur 1px</div>
<div class="bw2">Épaisseur 2px</div>

<!-- Coins arrondis -->
<div class="br1">Légèrement arrondi (2px)</div>
<div class="br3">Arrondi (8px)</div>
<div class="br-100">Cercle parfait (100%)</div>
<div class="br-pill">Pilule (9999px)</div>

<!-- Ombres -->
<div class="shadow-1">Ombre légère</div>
<div class="shadow-4">Ombre prononcée</div>

<!-- Opacité -->
<div class="o-50">50% opaque</div>
<div class="o-90">90% opaque</div>
```

## Responsive

Tachyons permet d'appliquer des classes différemment selon la taille d'écran grâce à des suffixes :

| Suffixe | Breakpoint | Largeur |
|---|---|---|
| _(aucun)_ | Tous écrans | — |
| `-ns` | Not Small | > 30em |
| `-m` | Medium | 30em – 60em |
| `-l` | Large | > 60em |

```html
<!-- Texte f6 sur mobile, f4 sur tablette, f2 sur grand écran -->
<h1 class="f6 f4-m f2-l">Titre responsive</h1>

<!-- Colonne pleine sur mobile, moitié sur grand écran -->
<div class="w-100 w-50-l">Contenu</div>

<!-- Flexbox activé seulement sur grand écran -->
<div class="flex-l">...</div>
```

## Avantages et limites

**Avantages :**
- Pas de conflits de nommage entre classes
- Le HTML est la source de vérité du style
- Taille du fichier CSS stable (n'augmente pas avec le projet)
- Idéal pour les systèmes de design et les prototypes rapides

**Limites :**
- HTML plus verbeux
- Difficile à lire si les classes ne sont pas connues
- Peu adapté si l'équipe préfère garder style et structure séparés

> Cette approche a inspiré des frameworks modernes comme **Tailwind CSS**, qui suit les mêmes principes avec une configuration plus poussée.

## Documentation officielle

La documentation complète de Tachyons (toutes les classes, palettes, exemples interactifs) est disponible sur : **https://tachyons.io/docs/**

---

# Exercices pratiques

## Exercice 1 : Styliser une page HTML

- Ajouter des couleurs et polices à une page HTML existante.

## Exercice 2 : Construire une mise en page responsive

- Utiliser Grid pour créer un layout.
