+++
title='Générateurs HTML'
url = "/generateurs_html"
+++

# Générateurs de Sites Statiques : Jekyll et Hugo

Les générateurs de sites statiques (SSG) comme **Jekyll** et **Hugo** permettent de construire des sites web performants, sécurisés et faciles à déployer. Ces outils transforment des fichiers statiques (Markdown, HTML, CSS) en sites web complets prêts à être hébergés.

---

## Pourquoi choisir un générateur de site statique ?

### Avantages :

- **Performance** : Les sites statiques se chargent plus rapidement car ils ne dépendent pas d'une base de données.
- **Sécurité** : Pas de backend ou de base de données signifie moins de vulnérabilités.
- **Facilité de déploiement** : Les sites générés peuvent être hébergés sur des plateformes comme GitHub Pages, Netlify ou Vercel.
- **Simplicité** : Écrire du contenu en Markdown est simple et intuitif.

### Inconvénients :

- **Moins adapté aux sites dynamiques** : Les fonctionnalités comme les commentaires ou les recherches avancées nécessitent des solutions tierces.
- **Courbe d'apprentissage** : Comprendre la configuration initiale peut être un obstacle.

---

## Jekyll

[Jekyll](https://jekyllrb.com/) est un SSG écrit en Ruby et très populaire, notamment grâce à son intégration avec GitHub Pages.

### Points clés :

- **Langage** : Ruby.
- **Configuration** : Fichier `_config.yml`.
- **Formats pris en charge** : Markdown, HTML.
- **Avantages** :
  - Parfait pour les blogs.
  - Large choix de thèmes prêts à l'emploi.
  - Intégration native avec GitHub Pages.

### Utilisation basique :

1. **Créer un nouveau projet :**
   ```bash
   jekyll new mon-site
   ```
2. **Lancer le serveur local :**
   ```bash
   bundle exec jekyll serve
   ```
3. **Construire le site :**
   ```bash
   jekyll build
   ```

Pour en savoir plus, visitez la [page dédiée à Jekyll](7_cours_jekyll.md).

---

## Hugo

[Hugo](https://gohugo.io/) est un SSG écrit en Go et réputé pour sa rapidité et sa flexibilité.

### Points clés :

- **Langage** : Go.
- **Configuration** : Fichier `config.toml`, `config.yaml` ou `config.json`.
- **Formats pris en charge** : Markdown, HTML.
- **Avantages** :
  - Temps de génération extrêmement rapide.
  - Idéal pour les sites volumineux.
  - Large bibliothèque de thèmes.

### Utilisation basique :

1. **Installer Hugo :**
   ```bash
   brew install hugo # macOS
   sudo apt install hugo # Linux
   ```
2. **Créer un nouveau projet :**
   ```bash
   hugo new site mon-site
   ```
3. **Lancer le serveur local :**
   ```bash
   hugo server
   ```
4. **Construire le site :**
   ```bash
   hugo
   ```

Pour plus de détails, consultez la [page dédiée à Hugo](8_cours_hugo.md).

---

## Comparaison entre Jekyll et Hugo

| Fonctionnalité              | Jekyll                 | Hugo                      |
| --------------------------- | ---------------------- | ------------------------- |
| **Langage**                 | Ruby                   | Go                        |
| **Facilité d'installation** | Moyen (Ruby requis)    | Facile (binaire portable) |
| **Vitesse de génération**   | Moyenne                | Très rapide               |
| **Thèmes**                  | Large choix            | Large choix               |
| **Communauté**              | Très active            | Très active               |
| **Hébergement**             | GitHub Pages (intégré) | Compatible Netlify, etc.  |

---

## Ressources supplémentaires

- [Liste des générateurs de sites statiques](https://www.staticgen.com/)
- [Guide Hugo officiel](https://gohugo.io/documentation/)
- [Guide Jekyll officiel](https://jekyllrb.com/docs/)
