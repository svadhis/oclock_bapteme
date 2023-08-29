# Correction MCD (rendu en retard)

Tu as fait un bon travail, la plupart des relations sont correctement définies et tu as pu identifier les entités à modéliser. Voici quelques points qui peuvent être améliorés :

- La relation *LIKE* entre **USER** et **PRODUCT** est optionnelle. Tu l'as correctement définie comme une relation Many-to-many, les cardinalités sont donc **0, N** des deux côtés.
  - Un utilisateur peut n'aimer aucun produit (**0**) comme en aimer 42 (**N**).
  - Un produit peut n'intéresser personne (**0**) comme en intéresser 404 (**N**).

- Il te manque surement des propriétés dans plusieurs entités, comme le nom de l'utilisateur pour la livraison. Prends le temps de bien réfléchir à toutes les informations dont tu as besoin pour chaque entité. Différencieras tu l'adresse de livraison de l'adresse de facturation ?

- Concernant les commandes, c'est un cas spécifique pour lequel on a besoin d'**informations précises et immuables**, ce qui n'est pas compatible avec ton modèle.

  Tu as défini une propriété total_amount dans ORDER. C'est bien, car si demain le prix des mugs augmente, le montant de la commande reste inchangé. Mais que se passe-t-il si tu as des mugs a des prix différents, et qu'un utilisateur te demande un remboursement pour un mug arrivé cassé sur sa commande de 31 mugs différents ?

  > *« Je bois beaucoup de café et j'aime bien avoir un mug différent*
  > *chaque jour du mois »*

  En l'état, tu n'as aucun moyen d'avoir le prix du mug au moment de la commande. Et comment pourrais tu éditer une facture détaillée avec les informations que tu as ?

  Il est important d'enregistrer toutes les informations d'une commande. Pour chaque produit commandé, il faut pouvoir connaitre la quantité achetée et le prix au moment de la commande.

  Tu peux ajouter une entité, **ORDER_LINE** ou **ORDER_ELEMENT**, qui contiendrait les informations relatives à un produit commandé. Elle fait le lien entre **ORDER** et **PRODUCT**, je te laisse réfléchir aux propriétés qu'elle contient et aux relations avec les autres entités.

- Enfin, comment vas-tu définir l'adresse de livraison (et facturation) à utiliser pour une commande ? Est-ce qu'il s'agit d'une information qui doit rester **immuable** pour une commande ? 🤔