# Feedback Parcours S6 - Apprenant 3

Bonjour Apprenant 3, voilà mon feedback à ta demande concernant ton parcours de S6.

Je vois que malgré la correction, tu n'as pas encore réussi à aller au bout de l'exercice. Rassures-toi cependant, je pense que tu es sur la bonne voie pour y arriver !
Le code est globalement clair et propre, ce qui est fait est assez bien fait. Mon sentiment est que tu as bien compris certaines notions qui étaient au coeur de ce parcours comme la POO et l'architecture MVC.
En revanche tu as été gêné par quelques notions dont ta maîtrise est un peu plus fragile et qui t'ont certainement empêchées d'aller plus loin.

## Attention au copier-coller

Il n'y a pas trop de traces d'autres projets dans ton code. On vous incitait à réutiliser du code d'Oshop mais en l'adaptant complètement à ce nouveau projet.
De ce côté là, je te félicite, je n'ai trouvé des restes d'Oshop que dans quelques commentaires. Je pense que le copier-coller a été fait intelligemment et je constate que tu n'a copié que ce dont tu avais besoin, au moment ou tu en as eu besoin.
C'est bien de laisser des commentaires du code que tu as copié au début, car il peut te donner des indications sur comment réutiliser le code que tu as récupéré. En revanche n'oublies pas de les retirer à la fin pour ne pas polluer ton projet avec des choses qui n'ont pas à voir avec celui-ci.

En revanche, tu es peut-être allé un poil vite en reprenant ce que tu avait fait pour les profs pour l'utiliser sur les élèves, et inversement. Je peux te citer le bouton pour ajouter un prof qui nous emmène sur la page d'ajout d'élève, la colonne titre dans la liste des élèves qui n'est utilie que pour les profs.

Un autre exemple plus marquant est celui de ta méthode pour ajouter un prof dans `TeacherController` qui s'appelle `studentAdd()` et fait appel à une variable `$newStudent` qui n'est pas définie. Cet exemple-ci est plus criant car VSCode souligne la variable qui pose problème ! N'oublie pas que VSCode est ton ami, et qu'il a toujours raison (ou presque) lorsqu'il te souligne une erreur !

## Templates de vues

Tu n'as pas suffisamment profité de la possibilité de créer des templates de vues qu'offre PHP. En effet, la méthode `show` de ton `MainController` fonctionne, mais elle n'effectue l'affichage que d'un template à chaque fois qu'on l'appelle.

Pour rappel, l'intérêt des templates est de construire une vue complète à partir de morceaux (les templates) qui peuvent se répéter d'une page à l'autre. Typiquement on créé un template pour le header, le header, et pour le contenu de chaque page. Ainsi la méthode show appelle dans cet ordre les templates : header, contenu, footer.
Cela permet d'avoir d'avoir le header et le footer sur toutes les pages, donc notamment d'avoir la navbar dispo partout sur le site !

En l'état, voilà ce que tu peux faire pour y remédier :

- Depuis le template de la page d'accueil, récupère tout le code qu'on va répéter, à savoir :
  - Pour le header, tout le début du code, incluant l'en-tête du document HTML, et la navbar. Tu peux même inclure la balse ouvrante `<div class="container my-4">` qui est là pour englober le contenu de la page et lui ajouter des marges.
  - Pour le footer, toute la fin du code, incluant la balise fermante de la div citée précédemment, les balises `<script>` (ce sont les fichiers javascript de bootstrap), les balises fermantes `</body>` et `</html>`.
- Ces deux fragments de codes seront à placer dans des fichiers .tpl.php dédiés respectivement au header et au footer. Tu peux t'inpirer de l'arborescence de la correction pour savoir ou les mettre.
- Ensuite il faut ajouter des require dans ta méthode `show` afin d'inclure systématiquement ces deux templates en plus du template principal de chaque page, le tout dans le bon ordre.
- N'oublie pas pour finir de retirer le header et le footer des templates de pages ou ils sont déjà présents, afin de ne pas faire doublon avec les templates que tu viens de créer.

A l'avenir, je te conseille de mettre en place des templates pour tes headers et footers assez tôt dans ton projet. Dans ce cas précis, cela va te permettre de disposer de la navbar sur n'importe quelle autre page, ce qui est très pratique pour pouvoir naviguer et tester le code des différentes pages au fur et à mesure qu'on avance !

## Fonctionnalité d'ajout de prof/élève

Comme tu n'as pas terminé cette étape, je vais te proposer des pistes de choses qui manquent à ton code pour que cette fonctionnalité soit opérationnelle. Je t'invite à utiliser mes commentaires en parallèle de la correction pour bien situer ce qui bloque.

Je prends l'exemple de l'ajout d'élève car c'est celui des deux ou tu es le plus proche du but. Une fois que celle-ci fonctionnera, tu devrais sans problème pouvoir te débrouiller pour les professeurs. Le vrai noeud bloquant, c'est qu'il faut prendre en compte le fait qu'un élève doit se faire assigner un prof :

- Pour pouvoir sélectionner un prof à assigner à l'élève, tu vas devoir donner la liste des professeurs à la vue du formulaire d'ajout d'élève. En enregistrant `Teacher::findAll()` dans une variable que tu transmets à la vue via la méthode show (comme tu l'as fait pour `$errorList` et `$newStudent`), tu y auras accès dans le template de la vue.
- Une fois la liste des profs transmise à la vue, tu vas pouvoir afficher dynamiquement les options dans le select correspondant. Tu peux pour ca boucler sur la liste, et pour chaque prof, ajouter une `<option>` avec son id en `value` et son nom en texte.
- Il manque la propriété `teacher_id` à ton modèle `Student`. Bien qu'il s'agisse d'une clé étrangère, teacher_id doit bien faire partie des propriétés de la classe. Par ailleurs, on ne pourra pas enregister un élève sans `teacher_id` car ce champ n'est pas nullable dans la table `student` de la base de données. Il faut donc ajouter cette propriété au modèle, ainsi que le getter et le setter associés.
- Pour finir, il faut récupérer l'id du prof sélectionné dans le formulaire depuis `$_POST` au moment de l'envoi du formulaire, et ne pas oublier de l'assigner à l'objet  à la bonne propriété de l'objet `Student` avant de l'enregistrer de pouvoir l'enregistrer en base de données.

## Conclusion

Dans l'ensemble c'est plutôt positif. Tout n'est pas parfait mais tu as déjà pris des bonnes habitudes et je ne pense pas qu'il y ait de notion à côté de laquelle tu serais passé complètement.
Je te conseille de reprendre la correction et d'essayer de finir au moins l'exercice principal (et quelques bonus si tu as le temps), en essayant de reprendre mes commentaires ci-dessus.

N'hésite pas à t'entraîner aussi sur les templates et la dynamisation des vues en reprenant d'anciens challenges.

Dernier petit conseil, dans un nouveau projet, commence par des choses qui peuvent t'aider et gagner du temps pour la suite. Typiquement, le fait d'avoir une barre navigation fonctionnelle sur toutes tes pages t'aurait sûrement aidé à tester plus efficacement ton code !