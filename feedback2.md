
# Feedback : Triple Triad Deck Builder

Je vois que tu as essayé d'intégrer toutes les fonctionnalités demandées dans le parcours. C'est très bien, mais il ne faut pas pour cela négliger le résultat. Il faut que chaque fonctionnalité soit complète et fonctionne comme prévu. Essaye d'aller au bout de la consigne et d'avoir un résultat satisfaisant avant de passer à la suite.

Ton rendu manque de soin. Je ne parle pas de faire du joli bien sur, ce n'était pas le sujet de ce parcours. Mais il faut un minimum, pour que l'utilisateur ne fasse pas une drôle de tête en naviguant sur ton site.

- 🤔 J'ai eu besoin d'aller voir ton code pour comprendre à quoi faisait référence le chiffre affiché dans les détails d'une carte
- 🫠 Le deck est présenté sous forme de tableau HTML avec une colonne pour la carte et une colonne toujours vide

Je vois que tu as réutilisé du code pour l'affichage du deck. C'est cool, on peut réutiliser du code, mais il faut bien prendre le temps de **comprendre** le code qu'on réutilise et de **l'adapter** correctement à la situation.

Sur la recherche par élément, voici la requête SQL que tu as utilisé :
```sql
SELECT * FROM card WHERE element IS NOT NULL
```
Le premier problème évident, c'est que cette requête ne sélectionne que les cartes qui ont un élément, mais tu utilises cette même requête pour afficher les cartes qui n'ont pas d'élément. Ca ne peut pas fonctionner.

Ensuite, pour les recherches avec élément, tu filtres le résultat en Javascript. C'est ok, ça fonctionne dans ce cas précis, avec une base de données réduite. Mais tu seras amené à travailler avec de bien plus grosses bases, et cela peut causer des soucis de performance. Le langage SQL est très complet et te permet de filtrer avec une grande précision les données dont tu as besoin.

> 💡 Essaye de faire plus attention à la façon dont tu nommes les
> paramètres dans les fonctions de callback que tu utilises. Il faut que
> ton paramètre reflète la nature de l'élément qu'il représente.
>
> ```javascript
> // deckController.js:16
>
> const foundDeckCard = req.session.deck.find((deck) => deck.id === id);
> ```
>
> Si tu devais expliquer cette ligne de code, tu dirais quelque chose
> comme : "*Dans le **deck** de la session, on trouve la **carte** dont
> l'id est égal à celui de la carte à ajouter*".
>
> ```javascript
> const foundDeckCard = req.session.deck.find((card) =>
> card.id === id);
> ```
>
> Egalement, Il faut bien faire attention à utiliser le **singulier** pour le
> paramètre.
>
> ```javascript
> // searchController.js:11
>
> const results = cards.filter(cards =>
> cards.element.includes(cardElement))
> ```
>
> Le paramètre dans la fonction représente **un élément** du tableau.
> C'est le cas pour beaucoup de méthodes Javascript sur les tableaux
> telles que find, map ou forEach.
>
> ```javascript
> const results = cards.filter(card =>
> card.element.includes(cardElement))
> ```
>
> Fonctionnellement, c'est pareil. Tu peux bien nommer ton paramètre
> **artichauds** que le code fonctionnerait tout aussi bien. Mais pour toi qui dois
> travailler et revenir sur ce code plus tard, chaque entité correctement nommée
> fera une grande différence sur la compréhension que tu peux avoir de ce code,
> et t'évitera bien des maux de tête ! Le conseil vaut pour tout ce qui est nommable
> bien sur (variables, classes, fonctions etc) 😉

**Tu es sur la bonne voie ! Tu fais preuve d'engagement, c'est très bien. En faisant preuve d'un peu plus de rigueur, autant dans le code que sur le rendu, tu pourras avoir un bien meilleur résultat.**