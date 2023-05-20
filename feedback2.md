# Feedback Parcours S6 - Apprenant 2

Bonjour Apprenant 2, voilà mon feedback à ta demande concernant ton parcours de S6.

Je constate que malheureusement, tu n'es allé que jusqu'à l'étape 4 de ce parcours.
Ce n'est pas beaucoup, mais il y a une bonne nouvelle : Je trouve le code que tu as produit est vraiment de très bonne qualité ! Il n'y a pas une miette de code superflu, il est très clair et succinct, tu as su utiliser les méthodes statiques, afficher dynamiquement la page active dans la navbar, etc.

Bref, c'est peut-être peu de choses faite, mais elles sont vraiment bien faites !

La seule remarque que je puisse te faire sur la clarté du code, c'est l'indentation dans `TeachersController` qui est un peu hasardeuse. J'ai cru pendant un instant que la méthode add se trouvait à l'intérieur de la méthode list. Tout le reste est impeccable et je devine que l'indentation en général n'est pas un problème pour toi puisqu'elle est bien partout ailleurs.

## Apprendre à gérer son temps

Le principal conseil que je puisse te donner, c'est d'essayer de mieux gérer ton temps.

A vue de nez, on peut dire que tu as réalisé environ 50% de l'exercice avec un code d'une qualité proche des 100%. C'est déjà pas mal et cela montre que tu possède déjà une certaine rigueur et que tu te poses les bonnes questions en codant.

Cependant, en pendant l'apothéose et plus tard en entreprise, il faudra aller assez vite, parfois un peu au détriment de la qualité. Evidemment il ne s'agit pas de coder à l'arrache pourvu que ca fonctionne, mais en baissant le curseur de qualité à 90 ou 80%, tu aurais peut-être pu aller beaucoup plus loin dans l'exercice.

As-tu utilisé des copier-coller d'Oshop comme on vous l'as conseillé dans l'énoncé ? Je pense que tu es quelqu'un de suffisamment rigoureux pour utiliser le copier-coller à bon escient, sans copier de choses inutile et en adaptant le tout à ton projet en cours.

## Améliorer tes templates de vues

Quelques petits commentaires sur la partie HTML des vues :

- Si tu fais tourner le code de la correction sur ta machine, tu remarqueras que l'affichage des éléments principaux est plus étroit et centré sur la page, là ou chez toi ces éléments prennent toute la largeur de l'écran. Tu peux y remédier en allant chercher ta `<div class="container my-4">` dans ton fichier `home.tpl.php`, et en mettant la balise ouvrante de cette div tout à la fin de ton template header, et la balise fermante tout au début de ton footer. C'est cette balise qui ajoute les marges sur les côtés grâce à la classe css de Bootstrap `my-4`.
- Dans la vue de la liste des profs, il y a un problème sur le bouton pour éditer un prof qui ne pointe pas vers le bon lien. Une fois la fonctionnalité d'édition en place, il faudrait que le bouton nous mène vers l'adresse de la route pour l'édition, et non pas celle de l'ajout d'un prof. Idéalement, on voudrait avoir un bouton "ajouter un prof" au dessus de la liste.
- Je vois que tu as cherché à mettre en surbrillance le lien actif dans la navbar. J'espère que tu n'as pas trop passé de temps là-dessus au détriment du reste, car même si c'est un détail qui fait plaisir quand il est bien fait, ça reste un détail.
Si toutefois je peux te conseiller là dessus : au lieu de comparer strictement `$viewData["currentPage"]` à une string, regarde si tu ne peux pas comparer plutôt le début de l'adresse avec un début de route. Par exemple tu peux ajouter l'attribut `active` sur le lien vers les profs à chaque fois que l'adresse courante commence par `/teachers`.
Par ailleurs, essaies d'utiliser des `===` en priorité plutôt que des `==`. Personnellement, j'ai l'habitude de n'utiliser par défaut que `===`, et `==` uniquement si je sais que j'ai une bonne raison de le faire (et franchement, c'est rare).

## Conclusion

Pour le prochain feedback assure-toi d'avoir bien retravaillé le parcours à l'aide de la correction. Le fait que tu n'aies pas plus avancé dans l'exercice malgré que vous ayiez eu la correction entre temps me laisse penser que tu n'as peut être pas pris suffisamment de temps pour retravailler ton parcours avec ce support.

N'hésite pas également à me poser des questions, par exemple en les laissant sous forme de commentaire dans le code. Comme tu as produit assez peu de code, mais de très bonne qualité, c'est compliqué pour moi d'identifier les points sur lesquels du as rencontré des difficultés et sur quoi je peux t'aider.

Pour finir, j'insiste sur l'importance d'apprendre à gérer son temps. C'est une question d'équilibre entre bien faire et faire beaucoup qu'il faut apprendre à jauger. Il n'y a pas de honte ni de contre-indication au copier-coller quand on sait ce qu'on fait !

Si ça peut te rassurer, je pense qu'il sera assez naturel pour quelqu'un de rigoureux comme toi d'apprendre à accélérer dans son travail. Accroches-toi et tâches d'y penser, et je pense que ça viendra tout seul !
