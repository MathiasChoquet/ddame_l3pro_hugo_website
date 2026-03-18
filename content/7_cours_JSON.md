+++
title='JSON'
url = "/json"
+++

JSON (JavaScript Object Notation) est un format texte pour stocker et échanger des données. Il est lisible par les humains et les machines, et est très utilisé sur le web.

---

# 1. À quoi ressemble du JSON ?

Un objet JSON associe des **clés** à des **valeurs**, entre accolades `{}`.

## Exemple :

```json
{
  "prenom": "Alice",
  "age": 22,
  "etudiante": true
}
```

---

# 2. Les clés et les valeurs

- La **clé** est toujours entre guillemets doubles `"..."`.
- Elle est séparée de la valeur par deux-points `:`.
- Les paires sont séparées par des virgules `,`, sauf la dernière.

## Exemple :

```json
{
  "ville": "Toulouse",
  "code_postal": 31000
}
```

---

# 3. Les types de données

| Type    | Exemple           |
| ------- | ----------------- |
| Texte   | `"Bonjour"`       |
| Nombre  | `42` ou `3.14`    |
| Booléen | `true` ou `false` |
| Null    | `null`            |
| Tableau | `[1, 2, 3]`       |
| Objet   | `{"a": 1}`        |

## Exemple :

```json
{
  "nom": "Bob",
  "note": 14.5,
  "admis": true,
  "commentaire": null
}
```

---

# 4. Les tableaux

Un tableau regroupe plusieurs valeurs entre crochets `[]`.

## Exemple :

```json
{
  "couleurs": ["rouge", "vert", "bleu"],
  "notes": [12, 15, 9, 17]
}
```

---

# 5. Tableaux d'objets

Un tableau peut contenir plusieurs objets — utile pour une liste de personnes, de produits, etc.

## Exemple :

```json
{
  "etudiants": [
    { "prenom": "Alice", "age": 22 },
    { "prenom": "Bob", "age": 24 },
    { "prenom": "Clara", "age": 21 }
  ]
}
```

---

# 6. Les erreurs courantes

```json
{ "nom": "Alice" }
```

**Erreur** : la clé doit être entre guillemets doubles → `"nom"`.

```json
{ "nom": "Alice", "age": 22 }
```

**Erreur** : pas de virgule après la dernière valeur.

```json
{ "nom": "Alice" }
```

**Erreur** : JSON n'accepte que les guillemets doubles `"..."`.

---

# 7. Exemple complet

```json
{
  "formation": "L3 Pro DDAME",
  "annee": 2026,
  "diplome_reconnu": true,
  "responsable": null,
  "matieres": ["HTML", "CSS", "JSON", "Hugo"],
  "coordonnees": {
    "universite": "Université Toulouse Jean Jaurès",
    "ville": "Toulouse",
    "code_postal": 31058
  },
  "etudiants": [
    {
      "prenom": "Alice",
      "age": 22,
      "moyenne": 14.5,
      "admise": true,
      "commentaire": null,
      "matieres_suivies": ["HTML", "CSS", "JSON"]
    },
    {
      "prenom": "Bob",
      "age": 24,
      "moyenne": 11.0,
      "admis": false,
      "commentaire": "doit repasser une épreuve",
      "matieres_suivies": ["HTML", "JSON"]
    }
  ]
}
```

# Ressources supplémentaires

- [Introduction à JSON — MDN](https://developer.mozilla.org/fr/docs/Learn/JavaScript/Objects/JSON)
- [Valider son JSON — JSONLint](https://jsonlint.com/)
- [Visualiser son JSON — JSON Crack](https://jsoncrack.com/)

---
