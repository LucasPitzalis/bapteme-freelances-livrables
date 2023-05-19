# Feedback Parcours S6 - Apprenant 1

Bonjour Apprenant 1, voilà mon feedback à ta demande concernant ton parcours de S6.
Dans l'ensemble c'est un bon parcours, quasiment tout ce que tu as codé jusque là fonctionne, le code est relativement succin et propre. Tu as même attaqué une bonne partie des bonus, c'est super !

Un certain nombre des points que je vais soulever relèvent de la qualité et de la clarté du code plutôt que de la question de son bon fonctionnement. En entreprise, tu seras amené à reprendre du code produit par d'autres, et à l'inverse, tes collègues pourront parfois continuer ce que tu as commencé. Du coup, garder un propre lisible et bien organisé aidera tout le monde à économiser du temps et des neurones dans ce genre de cas !

Je cite quelques un de ces points ici puisqu'ils s'appliquent à l'ensemble de ton travail :

- Pense à bien utiliser le camelCase dans les noms de variables/fonctions qui contiennent plusieurs mots. Ca na l'air de rien mais ça aide vraiment pour les noms à rallonge, donc autant prendre la bonne habitude.
- Les noms des variables et fonctions que tu déclares doivent au maximum être explicites. Par exemple, ta méthode `teacher` de `TeacherController`, sert à récupérer la liste de tous les profs et à les afficher dans la vue correspondante. Tu pourrais renommer cette méthode `list` par exemple.
Autre exemple, à l'intérieur de cette même méthode, ta variable `$teacher` qui contient la liste de tous les profs. Cela porte à confusion car tu écris teacher au singulier alors qu'il s'agit d'un tableau contenant l'ensemble des profs. `$teacherList` ou `$teachers` me paraissent plus appropriés.
- Si tu laisses des commentaires dans le code, assures toi qu'ils sont clairs et pertinents. Tu as parfois laissé en commentaire la même description pour des choses différentes (méthode d'afficahge d'un formulaire et méthode gérant le traitement de celui-ci), ce qui peut porter à confusion. D'ailleurs, les commentaires, ça n'est pas obligatoire. Si tu estimes par exemple que les noms des méthodes sont suffisamment explicites pour comprendre leur utilisation, tu peux t'abstenir de commenter.
- Essaie d'utiliser `===` au maximum plutôt que `==`. Pour rappel, `===` compare aussi le type, ce que ne fait pas `==`. Typiquement `"1" === 1` est `false` alors que `"1" == 1` est `true`. Personnellement, j'ai l'habitude de n'utiliser par défaut que `===`, et `==` uniquement si je sais que j'ai une bonne raison de le faire (et franchement, c'est rare).

## Routes

J'ai 2 petits points à soulever au niveau de ton mapping des routes de l'app :

- Au moment de déclarer les routes dans ton `index.php`, tu pourrais les regrouper par entité plutôt que les laisser dans l'ordre dans lequel tu les ajoutées. Je t'invite à t'inspirer du fichier `app/routes.php` de la correction, où on a d'abord les routes pour les étudiants, puis les profs, etc.
- Essaie de garder la cohérence dans les chemins et les noms des différentes routes, notamment le pluriel/singulier des noms d'entités. Dans les noms des routes, tu as nommer les entités au singulier (teacher, student), par contre dans les chemins, il y a tantôt du pluriel, tantôt du singulier. Par exemple certaines des routes pour les profs commencent par `/teachers` (list, add) et d'autres par `/teacher` (update, delete). Les deux sont corrects, mais idéalement il faudrait avoir la même chose partout. Puisque les noms de tes routes utilisent les singuliers, le plus simple serait de changer tous tes chemins au singulier !

## Retour des méthodes dans les modèles

Globalement tes modèles sont très bien, j'ai peu de choses à en dire. Il y a quand même une chose qui a attiré mon attention. Dans les méthodes de CRUD qui font autre chose que de la lecture (donc tes méthodes `insert`, `update` et `delete`), on veut généralement renvoyer `true` ou `false` selon si la modification en base de données a réussi ou échoué. Il y a certains cas (tes méthodes `delete`) ou tu retourne directement `true`, sans vérifier que l'action a fonctionné. 

Je t'invite à appliquer ce que tu as fait pour les autres cas (`update` et `insert`) pour retourner `true` si au moins une ligne de la BDD est modifiée ou `false` dans le cas contraire.

## PDO::exec vs PDOStatement::execute

Pour effectuer des actions sur la base de données, tu as parfois utilisé :

```php
$pdo->exec($sql);`
```

Et d'autres fois :

```php
$pdoStatement = $pdo->prepare(/* ... */);
$pdoStatement->execute(/* ... */);
```

A chaque fois que la requête doit prendre en compte un paramètre donnée par l'utilisateur (par exemple un id dans la barre d'URL ou la saisie d'un formulaire), je te conseille d'utiliser la seconde méthode, car elle est sécurisée contre les injections SQL.
Je t'invite à consulter [ce thread sur stackoverflow](https://stackoverflow.com/a/29719505) si tu veux approfondir cette notion.

## Méthodes statiques

Pour faire court, une méthode peut être déclarée comme statique avec l'ajout du mot clé `static` lorsqu'elle ne nécessite pas un objet existant pour être utilisée. Dans ce cas, tu peux appeler la méthode directement, sans instancier la classe.
A titre d'exemple, voilà comment tu pourrais réécrire ta méthode de `TeacherController` pour afficher la liste des profs (et j'en profite pour prendre en compte mon commentaire sur les noms de variables explicites !) :

```php
public function list()
{
    $teacherList = Teacher::findAll();
    
    $this->show("teacher/teacher_list", [
        'teachers' => $teacherList
    ]);
}
```

Puisque la méthode `findAll()` de la classe `Teacher` est statique, je peux directement l'appeler sans avoir à instancier la classe avec `new Teacher()` !

## Permissions

Je passe rapidement sur cet aspect car il me semble que tu as bien compris comment faire ici. J'ai deux petites remarques :

- Je te conseille de faire à nouveau à la lisibilité dans le tableau `$acl` ou tu définies les autorisations par route. Tu peux regrouper les routes par entité comme je te l'ai suggéré pour le mapping des routes. Les routes ouvertes à tous les utilisateurs n'ont pas besoin d'être listées. Si tu veux épurer encore un peu plus ton code, tu peux retirer les routes laissées en commentaire (à moins que tu ne souhaite les laisser pour pouvoir y ajouter plus facilement des autorisations plus tard).
- La liste des profs est censée être accessible au role `user`, c'est précisé dans l'énoncé du parcours. Je suppose que c'est une simple erreur d'inattention, et je pense que suivre le conseil précédent t'aurait aider à la repérer ;)
- Lorsque l'accès est refusé à l'utilisateur dans la méthode `checkAuthorization`, tu répètes du code que tu as déjà dans ton `ErrorController`. Tu pourrais de contenter d'un appel à la méthode `error403` de ce contrôleur.

## Fonctionnalité de modification des profs et élèves

Je note que pour le moment cette fonctionnalité n'est pas correctement implémentée. Cela faisait partie des bonus, donc pas d'inquiétude, c'est déjà bien d'en être arrivé là !
J'ai vu qu'il y a quelques petites erreurs dans tes methodes `teacherUpdatePost` et `studentUpdatePost`, ainsi qu'une indentation un peu bizarre. Je devine qu'il y a eu surtout un début de copier-coller qui n'a pas encore abouti à quelque chose de propre :)

Pour te débloquer sur cette fonctionnalité :
Tu n'as pas besoin de de remplir l'attribut `action` de la balise `<form>` de ton formulaire (et c'est valable aussi pour les formulaires d'ajout). Si j'ai bonne mémoire, laisser `action` vide (ou ne carrément pas le mettre) permet d'envoyer le formulaire à la même adresse. Ca tombe bien, puisque la route post qui traite le formulaire a justement la même adresse que la route get qui permet de l'afficher !

Si tu voir des choses un peu avancées, je te recommande de regarder dans la correction des formulaires. Tu verras notamment comment présélectionner dynamique une option sur un `<select>`, et comment on peut factoriser les formulaires d'ajout et de modification en un seul template !

## Conclusion

La plupart de mes remarques ont vocation à développer ta rigueur et la cohérence de ton code. Développer de bonnes habitudes peut te permettre de travailler plus facilement en équipe et d'optimiser ton code, donc c'est toujours intéressant.

Bon, j'ai été très bavard ! Mais rassures-toi, c'est bon signe. Tu as été plus loin que la plupart des autres apprenants, donc logiquement, qui dit plus de code dit plus de choses à dire. Quand bien même tu aurais fait tout ça a posteriori avec la correction, cela montre que tu as bien compris beaucoup de choses et que tu es très impliqué !
