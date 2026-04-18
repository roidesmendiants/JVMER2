# JVMERDE 

Big S/O aux kheys **BlackArch**, **Bakuredo**, **StrangerFruit**, **captain_cid31**, **herolink** et tous les débuggueurs du topic :ange: 

# Guide de modification

Ce guide recense **chaque élément visuel et comportemental** du script que tu peux modifier, avec la ligne exacte à changer et des exemples concrets. Tu n'as pas besoin de comprendre le code — tu repères ce que tu veux changer, tu trouves la ligne, tu modifies la valeur.

---

## Sommaire

- [Réglages rapides (CONFIG)](#réglages-rapides-config)
- [Messages dans les topics](#messages-dans-les-topics)
- [Liste des sujets](#liste-des-sujets)
- [Signatures](#signatures)
- [Boutons de citation / actions](#boutons-de-citation--actions)
- [Titre du topic](#titre-du-topic)
- [Pagination](#pagination)
- [Liens visités](#liens-visités)
- [Mise en page générale](#mise-en-page-générale)
- [Comportement de l'auto-refresh](#comportement-de-lauto-refresh)
- [Barre du bas](#barre-du-bas)

---

## Réglages rapides (CONFIG)

Le bloc `CONFIG` est **tout en haut du script**. C'est la zone prévue pour les réglages courants.

```js
const CONFIG = {
    fontSizeMessages: 17,    // ← taille du texte des messages (px)
    fontSizeTopics:   16,    // ← taille des titres dans la liste des sujets (px)
    fontSizeAuthor:   13,    // ← taille du pseudo dans la liste des sujets (px)
    autoRefreshMode: 'auto', // ← 'auto' | 'force' | 'notify'
};
```

---

## Messages dans les topics

### Taille du texte des messages

```js
// Dans CONFIG :
fontSizeMessages: 17,   // change 17 par la valeur souhaitée
```

### Espacement interne de chaque message (padding)

Cherche `.messageUser__msg` dans le CSS. Modifie `padding-left` et `padding-right` :

```css
.messageUser__msg {
    font-size: ${CONFIG.fontSizeMessages}px !important;
    padding-left: 5px !important;   /* ← espace à gauche du texte */
    padding-right: 5px !important;  /* ← espace à droite du texte */
}
```

> Augmente à `10px` ou `15px` pour plus d'air, mets `0px` pour coller aux bords.

### Espacement entre les messages

Cherche `.messageUser {` :

```css
.messageUser { margin-bottom: 4px !important; }
/*                             ↑ espace entre chaque message */
```

> `4px` = serré. `12px` = espacé. `0px` = collés.

### Masquer les cases à cocher de sélection

Par défaut elles sont cachées. Pour les réafficher, cherche :

```css
.messageUser__checkboxContainer { display: none !important; }
```

Remplace `none` par `flex` pour les faire réapparaître.

### Padding de la carte message

Cherche `.messageUser__card {` :

```css
.messageUser__card {
    padding: 4px 8px !important;  /* ← padding vertical / horizontal de la carte */
    ...
}
```

---

## Liste des sujets

### Taille et gras des titres de topics

```js
// Dans CONFIG :
fontSizeTopics: 16,   // change 16 par la valeur souhaitée
```

Ou directement dans le CSS, cherche `.tablesForum__subjectText` :

```css
.tablesForum__subjectText {
    font-weight: bold !important;   /* ← mettre 'normal' pour enlever le gras */
    font-size: ${CONFIG.fontSizeTopics}px !important;
}
```

> **Enlever le gras des titres :** remplace `bold` par `normal`.

### Taille du pseudo de l'auteur

```js
// Dans CONFIG :
fontSizeAuthor: 13,   // change 13 par la valeur souhaitée
```

### Masquer les avatars empilés et le séparateur

Ces éléments sont masqués par défaut. Pour les réafficher, cherche :

```css
.tablesForum__remainingAvatars, .tablesForum__separator { display: none !important; }
```

Remplace `none` par `block` (ou supprime la ligne entière).

### Décalage de la colonne "dernière réponse"

Cherche `.tablesForum__rowLastMsg` :

```css
.tablesForum__rowLastMsg { margin-left: 5px !important; }
/*                                      ↑ espace à gauche de "dernière réponse" */
```

---

## Signatures

Cherche `.messageUser__signature` dans le CSS :

```css
.messageUser__signature {
    margin-top: 10px !important;     /* ← espace au-dessus de la signature */
    padding-left: 0px !important;    /* ← retrait à gauche */
    font-size: 0.85em !important;    /* ← taille du texte (relatif au message) */
    margin-bottom: 0px !important;   /* ← espace en dessous */
}
```

> Exemples pour `font-size` : `0.75em` (plus petit), `1em` (même taille que le message), `12px` (taille fixe).

### Ligne de séparation au-dessus de la signature

Cherche `.messageUser__separator` :

```css
.messageUser__separator {
    border-top: 0.0625rem solid var(--border-color);
    width: 100%;
    margin-bottom: -2px;
}
```

> Pour **supprimer la ligne** : ajoute `display: none !important;` dans ce bloc.  
> Pour la rendre plus épaisse : change `0.0625rem` par `2px`.  
> Pour changer sa couleur : remplace `var(--border-color)` par ex. `#ff0000`.

---

## Boutons de citation / actions

Les boutons (citer, signaler…) sont semi-transparents par défaut et s'affichent au survol.

### Opacité des boutons au repos

Cherche `.messageUser__footer {` :

```css
.messageUser__footer {
    ...
    opacity: 0.5 !important;          /* ← 0 = invisible, 1 = toujours visible */
    transition: opacity 0.2s !important;  /* ← vitesse de l'apparition (secondes) */
}
```

> Mets `opacity: 1 !important;` pour que les boutons soient **toujours visibles**.  
> Mets `opacity: 0 !important;` pour qu'ils n'apparaissent **qu'au survol**.

### Espacement entre les boutons

Dans le même bloc `.messageUser__footer` :

```css
gap: 4px !important;   /* ← espace entre les boutons d'action */
```

---

## Titre du topic

Cherche `.titleMessagesUsers__title` :

```css
.titleMessagesUsers__title {
    font-size: 1.725rem !important;   /* ← taille du titre (ex: 1.5rem, 2rem, 24px) */
    line-height: 1.25 !important;     /* ← interligne si le titre tient sur plusieurs lignes */
    word-break: break-word !important;
}
```

---

## Pagination

### Espace sous la barre de navigation haute

Cherche `.container__navTop` :

```css
.container__navTop { margin-bottom: 4px !important; }
/*                                  ↑ espace sous la barre de navigation */
```

### Espace sous les numéros de page en haut

Cherche `.js-pagination-top.container__pagination` :

```css
.js-pagination-top.container__pagination { margin-bottom: 4px !important; }
/*                                                         ↑ espace sous la pagination haute */
```

---

## Liens visités

Les topics déjà lus apparaissent en gris. Pour changer cette couleur, cherche `a:visited` :

```css
.tablesForum__subjectText a:visited,
.tablesForum__subjectLink:visited,
a.tablesForum__subjectLink:visited,
.tablesForum__bodyRow a:visited { color: #777 !important; }
/*                                        ↑ couleur des topics visités */
```

> `#777` = gris moyen. `#aaa` = gris clair. `#999` = gris neutre. N'importe quelle couleur CSS fonctionne.

### Couleur des boutons de pagination visités

```css
a.pagination__button:visited {
    color: #aaa !important;         /* ← couleur du texte */
    border-color: #555 !important;  /* ← couleur de la bordure */
}
```

---

## Mise en page générale

### Largeur de la zone de lecture (écrans larges)

Cherche `@media (min-width: 1400px)` :

```css
@media (min-width: 1400px) {
    .layout { grid-template-columns: 1fr 55rem 24.5rem 1fr !important; }
    /*                                    ↑ largeur du contenu
    /*                                              ↑ largeur de la sidebar */
}
```

> Augmente `55rem` pour élargir la zone de lecture (ex. `65rem`, `70rem`).

### Largeur quand la sidebar est masquée

Ligne suivante dans le même bloc :

```css
body.jvmerde-nosidebar .layout { grid-template-columns: 1fr 80rem 1fr !important; }
/*                                                            ↑ largeur sans sidebar */
```

---

## Comportement de l'auto-refresh

### Fréquence de vérification

Cherche `REFRESH_DELAY` dans le script :

```js
const REFRESH_DELAY = 30000;
//                    ↑ délai en millisecondes (30000 = 30 secondes)
```

> `15000` = toutes les 15 secondes. `60000` = toutes les minutes.

### Mode de rechargement

```js
// Dans CONFIG :
autoRefreshMode: 'auto',   // 'auto' | 'force' | 'notify'
```

| Valeur | Comportement |
|---|---|
| `'auto'` | Recharge si en bas de page, sinon affiche une notif cliquable |
| `'force'` | Recharge toujours automatiquement |
| `'notify'` | Affiche juste un lien, ne recharge jamais |

### Marge de détection "en bas de page"

Cherche `isScrolledToBottom` :

```js
const isScrolledToBottom = () =>
    window.scrollY + window.innerHeight >= document.documentElement.scrollHeight - 150;
//                                                                                  ↑ marge en pixels
```

> Augmente `150` pour déclencher le rechargement automatique plus tôt quand tu approches du bas.

---

## Barre du bas

### Couleurs de la barre (thème sombre)

Cherche `#old-jvc-bar-v22 {` dans le CSS :

```css
#old-jvc-bar-v22 {
    background: #1e2125;        /* ← fond de la barre */
    border: 1px solid #32373d;  /* ← bordure */
    gap: 10px;                  /* ← espace entre les boutons */
    padding: 12px;              /* ← padding interne de la barre */
}
```

### Couleurs et style des boutons

Cherche `.btn-jvc-v22 {` :

```css
.btn-jvc-v22 {
    background: #32373d;        /* ← fond des boutons */
    color: #fff !important;     /* ← couleur du texte */
    border: 1px solid #454d55;  /* ← bordure des boutons */
    padding: 7px 15px;          /* ← padding vertical / horizontal */
    font-size: 13px;            /* ← taille du texte */
    border-radius: 3px;         /* ← arrondi des coins */
}
```

### Modifier les labels des boutons

Cherche `bar.innerHTML` dans le script :

```js
bar.innerHTML = `
    <a href="${forumUrl}" class="btn-jvc-v22">« Liste des sujets</a>
    <a href="#forums-post-message-editor" class="btn-jvc-v22">↩ Répondre</a>
    <a href="${forumUrl}#forums-post-topic-editor" class="btn-jvc-v22">✏ Nouveau sujet</a>
    <a href="javascript:location.reload();" class="btn-jvc-v22">Actualiser</a>
    <button id="jvmerde-toggle" class="btn-jvc-v22">⟳ Auto ON</button>
`;
```

> Change le texte entre les balises pour renommer un bouton.  
> Supprime une ligne `<a ...>` entière pour retirer un bouton.
