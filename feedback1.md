

# Feedback : Triple Triad Deck Builder

Le rendu est très bon, tant dans la présentation que dans les fonctionnalités. Les consignes sont bien suivies, les bonus faits, et le résultat est à la hauteur !

🐛 Il y a un petit bug qui traine : quand on recherche les cartes par élément, le titre de la page affiche **NaN** au lieu de l'élément en question. Il y a une coquille dans ton code : un "+" en trop dans le titre.

```javascript
res.render('main/cardList', {
cards: searchedResults,
title: 'Résultat de la recherche : '  + (searchedElement ===  'null'  ?  ' sans élément'  :  + searchedElement),
});
```

Les [template strings](https://www.w3schools.com/js/js_string_templates.asp) peuvent t'aider à y voir plus clair et éviter ce type d'erreurs en simplifiant la syntaxe. Tu les utilises déjà, notamment pour la recherche par niveau.

```javascript
res.render('main/cardList', {
cards: searchedResults,
title: `Résultat de la recherche : ${searchedElement  ===  'null'  ?  ' sans élément'  :  searchedElement}`,
});
```

Tu peux également décomposer ton code pour ne pas gérer les conditions et la concaténation sur une seule ligne. Au plus tu simplifies ton code, au plus tu évites les bugs.

```javascript
const  elementTitle  = searchedElement ===  'null'  ?  ' sans élément'  : searchedElement;

res.render('main/cardList', {
cards: searchedResults,
title: 'Résultat de la recherche : ' + elementTitle
});
```

Dans l'ensemble, ton code est efficace et bien organisé. C'est du bon travail !

> 💡 Tu peux améliorer la lisibilité de ton code en le nettoyant de tout
> ce qui ne sert pas. Je pense à certains **console.log**, au **code
> commenté** et au **code mort** (et aux **console.log morts commentés**
> 😊) que tu as pu laisser dans le projet alors qu'ils n'ont pas
> d'utilité. Cela peut parfois sembler trivial, mais une méthode qui
> n'est plus utilisée, comme ***dataMapper.searchByElementNull()*** ,
> peut induire en erreur le prochain développeur qui passera par là, y
> compris toi-même !

**Bravo pour ce parcours ! On voit que tu es à l'aise et que tu fais des efforts pour fournir un code de qualité, continue comme ça !**