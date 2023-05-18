# Correction MCD

Bonjour Apprenant, voilà une petite correction de ton MCD.

Dans l'ensemble le schéma et les entités sont clairs, les associations et les verbes qui les caractérisent font sens. On sent que tu as compris le principe du MCD et ce à quoi il doit ressembler.

## La question de l'id

Concernant les attributs `id` que tu as donné à toutes les entités : en principe dans un MCD, on indique pas l'id de cette manière. Comme son nom l'indique, le MCD est un modèle <ins>conceptuel</ins>, par opposition aux modèles plus concrets que sont le MLD et le MPD. Le MCD n'est donc pas censé représenter les objets tels qu'ils seront stockés en base de données, mais plutôt sous forme de concept logique compréhensible par à peu près tout le monde.

On préfère au terme `id`, qui est déjà un peu du jargon de dev, le terme `code` par exemple. Dans notre cas, cela peut donner `code_user`, `code_order`, etc.
Par ailleurs, ce code qui sera remplacé en `id` dans la base de donnée est ce qu'on appelle l'identifiant de l'objet, qui sert à le disinguer des autres objets du même type. Pour bien souligner son rôle particulier, on a tendance à le souligner dans la liste des attributs.

## Attribut superflu

J'ai un petit commentaire concernant l'attribut `total_amount` de l'`entité order`. Selon moi, cet attribut n'est pas nécessaire. Si on a besoin de retourner le montant d'une commande, il suffira de récupérer tous les produits contenus dans celle-ci et de faire la somme de leurs prix à la volée. En faisant ainsi, on peut se passer de cet attribut ce qui peut nous éviter par exemple d'avoir à le mettre à jour si on ajoute/supprime un produit de la commande.

## Relation "Many-To-Many"

Autre point, sûrement le plus important : la relation `like`entre `user` et `product`. Comme tu l'as bien identifié, il s'agit d'une relation "Many-To-Many", puisqu'un utilisateur peut liker un ou plusieurs produits (qui peut être liké par un ou plusieurs utilisateurs). Cependant, les cardinalités que tu as indiqué ne correspondant pas à ce type de relation. C'est dommage, car il existe une autre relation de ce type dans ton MCD, qui est celle entre `order` et `product` et dont les cardinalités sont bonnes !
Je te propose de répondre ici à ce problème :

- Un utilisateur est libre de liker un ou plusieurs produits. La cardinalité à indiquer du côté de `user` est donc "0,N".
- Un produit peut être liké par aucun, un ou plusieurs utilisateurs. La cardinalité à indiquer du côté de `product` est donc "0,N" également.

## Mise en forme du schéma

Pour finir, j'ai quelques toutes petites remarques concernant la forme du schéma :

- Tu peux représenter les associations sous formes de tables, un peu de la même manière que les entités. En effet, bien que ce ne soit pas forcément utile dans le cas présent et je ne rentrerai pas dans les détails, mais il se trouve que les associations aussi peuvent avoir des attributs ! Les représenter sous forme de tables permet alors de lister ces attributs.
- Généralement, on essaie de donner une forme différente aux cases contenant les entités et les associations, afin de bien distinguer les deux. Le plus souvent, on met des coins arrondis sur les associations. Je chipote un peu car tu as déjà utilisé des couleurs pour différencier les deux, mais il est toujours intéressant d'avoir une idée des conventions répandues.

Pour t'éviter à trop penser à ces petits détails à l'avenir, je t'invite à réaliser tes prochains MCD avec un outil dédié. Je te recommande [Mocodo Online](https://www.mocodo.net/) qui permet de générer le MCD à partir d'un texte, de le mettre en forme comme on souhaite, et même de l'exporter sous différents formats ou encore de générer le MLD correspondant dans la foulée !
