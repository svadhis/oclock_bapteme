

# Fetch

La méthode **fetch()** te permet d'effectuer des requêtes HTTP directement depuis ton code Javascript. Tu fournis une url et les éventuels paramètres nécessaires, et tu obtiens une réponse en retour que tu peux utiliser dans ton code.

Voici à quoi ressemble un fetch :

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Erreur : ' + error));
```

Eh oui, le fetch est **asynchrone**. Voici le même avec la syntaxe **async/await** :

```javascript
async function fetchData(url) {
    try {
        let response = await fetch(url);
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Erreur : ' + error);
    }
}
```

Le fetch retourne une réponse HTTP. Elle contient de nombreuses informations, comme le statut de la requête, les headers, et les données. Nous pouvons gérer les erreurs en fonction de la réponse que l'on obtient. Les données doivent être converties pour les récupérer.

> Ici nous utilisons **response.json()** pour récupérer les données car
> nous attendons du JSON en réponse, mais nous pourrions recevoir
> d'autres types de données, comme du HTML par exemple. Dans ce cas,
> nous utiliserions la méthode **response.text()**.

Quand tu mets un simple lien **\<a>** ou un formulaire classique dans ton site, c'est le navigateur de l'utilisateur qui va s'occuper de "fetch" le serveur, récupérer la réponse, rediriger vers la page d'erreur le cas échéant, et charger entièrement une nouvelle page avec les données reçues (le HTML renvoyé par le serveur).

**Avec fetch(), c'est toi qui gère cela manuellement. Tu contrôles l'échange avec le serveur et la gestion de la réponse, et tu peux exploiter les données comme tu le veux sans avoir a quitter la page actuelle.**

> Fetch n'est pas reservé au front ! On l'utilise tout autant côté
> serveur pour communiquer avec d'autres sources. On a pas le choix
> d'ailleurs : il n'y a pas l'option navigateur sur notre serveur, on
> doit forcément gérer nous même cette communication !


## Exemple

Dans notre Deck Builder, on pourrait par exemple vouloir que les informations de la carte sur laquelle on clique s'affichent dans une popup au dessus de la liste de cartes au lieu de rediriger vers une autre page. Cela permettrait de pouvoir naviguer dans la liste de cartes plus facilement, sans avoir a repartir au début de la liste à chaque fois.

Dans notre controller, la méthode **renderOneCard** pourrait renvoyer les informations de la carte au format JSON.

```javascript
// res.render("card/card-item", { card })
res.json(card)
```

Nous pourrions récupérer ces données côté front avec un fetch.

```javascript
async function getCardDetails(id) {
	try {
		const response = await fetch(`${serverUrl}/card/${id}`);
		const card = await response.json();
		// card contient les données de la carte, on peut mettre à jour
		// le DOM avec ces données
	}
	catch (error) {
		console.error(error);
	}
}
```

Si tu souhaites approfondir sur le concept ou que ce n'est pas très clair, n'hésite pas à revenir vers moi !