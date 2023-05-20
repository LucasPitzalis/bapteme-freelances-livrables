# Feedback Parcours S6 - Apprenant 4

Bonjour Apprenant 4, voilà mon feedback à ta demande concernant ton parcours de S6.

Il y a pas mal de choses qui me paraissent correctes : les routes me semblent bien, elles correspondent globalement au méthodes présentes dans les contrôleurs, les templates attendus sont là (même si ils ne sont pas tous finis), les modèles me paraissent bon également.

Le gros problème c'est qu'en l'état, c'est difficile de pouvoir rentrer dans le détail pour en dire plus. La raison est que dès le départ, ton projet ne tourne pas.
Je pense que c'est un problème de méthode, et que tu as cherché à couvrir tout l'exercice d'un coup, à coup copier-coller, mais sans jamais (ou alors très rarement) vérifier que le code fonctionne.

## Teste, teste et reteste

<strong>Tester son code, c'est primordial.</strong>
C'est impossible de savoir si ton code fonctionne sans le tester, et c'est très compliqué de le réparer si tu ne teste qu'à la toute fin.
Coder tout d'un coup et croiser les doigts à la fin en espérant que ça marche, c'est une très mauvaise idée. Tu vas passer un temps fou à retrouver tes erreurs en faisant comme ça.

Ton code est parsemé de petites erreurs, oublis, at autres fautes de frappes qui me prouvent que tu as voulu en faire trop, tout d'un coup.
Il y a notamment beaucoup de moments ou tu appelles des variables, fonctions et classes avec des noms au singulier alors qu'ils sont déclarés au pluriel (ou inversement). Naturellement, si tu déclares la classe `Students` (au pluriel), PHP ne s'en sortira pas si tu essaies de l'instancier en faisant `new Student()` (au singulier).
C'est un type d'erreur que tu as fait de nombreuses fois et qui est parfois difficile à retrouver quand on a pas l'habitude, et encore plus si tu ne teste pas ton code.

Au passage, concernant les noms au pluriel et singulier, je te conseille de prendre l'habitude de choisir une fois lequel tu utilise et de faire en sorte de t'y tenir, pour éviter ce genre d'erreurs et maintenir une certaine cohérence. Une bonne astuce, c'est de ne jamais (ou presque) utiliser les pluriels. Comme ça, pas d'erreur ou d'incohérence possible. Et si tu as besoin d'un tableau ou d'une liste, utilise le mot "list". Par exemple, tu peux appeler la liste des professeurs `$teacherList`.

Tu as à ta disposition deux outils principaux pour éviter et débusquer les erreurs. Déjà, avant même de tester le code, tâche de prêter attention à ce que te signale VSCode. Je vois beaucoup de choses qu'il souligne en rouge dans ton code. Ce sont beaucoup des noms de variables, fonctions et classes que tu as mal tapés, recopiés mais pas remplacés ou carrément oublié de déclarer. Si VSCode te dit que quelque chose n'est pas défini, c'est qu'il y a un problème.

Ensuite, lorsque tu testes ton code, lis les messages d'erreur. A défaut de te dire directement ce qui ne va pas, un message d'erreur te donnera toujours une piste à remonter pour retrouver le problème. C'est parfois plus facile à dire qu'à faire, mais on finit par revoir passer toujours les mêmes messages et développer un instinct pour ces choses. Mais encore une fois, si tu ne testes pas, tu ne verras jamais les messages d'erreur ! Donc, tu sais ce qu'il te reste à faire ;)

## CoreController et méthode show

Voilà selon moi le plus gros problème qui empêche ton code d'afficher la moindre page.

Tous tes contrôleurs sont des classes enfant de la classe `CoreController` qui n'existe pas dans ton code. Dans la correction, tu peux notamment voir que c'est comme ça qu'ils héritent de la méthode `show()`. C'est cette méthode qui s'occupe d'afficher nos différents templates.

Tu vas donc devoir rajouter ce contrôleur et cette méthode afin de pouvoir afficher quelque chose. Je t'invite à retourner voir la correction pour t'en inspirer.
Prête attention notamment à la fin de la méthode qui appelle les différents templates par des `require` successifs, et aussi à la manière dont la méthode show transfère les informations à la vue avec le paramètre `$viewVars` afin d'afficher dynamiquement les contenus.

## Templates de vues

Tes templates m'ont l'air assez bien dans l'ensemble. Cependant je note que certains sont de vrais templates, et d'autres, des pages entières. Tu as oublié de créer les templates de header et de footer. Idéalement ces deux templates devraient être systématiquement affichés, respectivement avant et après le template de la page courante, afin de toujours avoir un header et un footer affichés.

Je t'invite à retourner voir la correction pour ces templates et les `require` à la fin de la méthode `show`.

## Méfiance avec le copier-coller

Tu as beaucoup fait de copier-coller. C'est flagrant. On trouve ci et là des choses qui ont étés copiées-collées mais pas toujours adaptées au projet en cours. Je pense par exemple à la méthode appelée par ta route `teachers` qui s'appelle `products`. Or cette méthode n'existe pas et son nom ne fait pas sens. Je devine que c'est un reliquat d'Oshop...

Certes, il était conseillé de réutiliser du code d'Oshop pour aller plus vite sur ce parcours, cependant, copier-coller ne rime à rien si on adapte pas complètement le code ou qu'on ne comprend pas ce qu'on recopie. La prochaine fois que tu seras amené à coder un projet qui ressemble beaucoup un à autre, je te conseille de changer de méthode.

Plutôt que de tout copier coller et parcourir le code pour l'adapter, fais comme si tu partais de zéro. Au fur et à mesure que tu avances, va consulter le code du projet d'origine pour t'en inspirer, et si tu trouves des morceaux de code qui te paraissent réutilisables, tu peux les recopier mais par petits bouts. Prends le temps d'adapter et tester le code au fur et à mesure, à chaque copier-coller.

## Conclusion

Je te le rappelle une dernière fois, il faut coder par petit bouts, et tester au fur et à mesure. C'est vraiment le meilleur conseil qu'on puisse donner à un dev à mon avis. Mais rassures-toi, il n'est jamais trop tard pour l'appliquer.

Je te conseille de retravailler ce parcours en t'aidant de la correction et des conseils que je t'ai donné. Pour développer de bonnes habitudes, je te recommande de repartir de zéro, en avançant petit à petit, fonctionnalité par fonctionnalité (suis bien l'ordre de l'énoncé et passe à la fonctionnalité suivante uniquement lorsque tu as fini la précédente), en testant, et en faisant attention au copier-coller.
Personnellement, j'aime bien recopier le code manuellement plutôt qu'utiliser le copier-coller. Ca permet de s'imprégner de la syntaxe qu'on copie, et d'adapter le code à la vollée plutôt que de rechercher après coup ce qu'il faut modifier.

Ton oubli d'ajouter le `CoreController` et la méthode `show()` me laissent penser que tu ne maîtrise peut-être pas complètement l'architecture MVC et/ou la notion d'hérédité des classes. Si c'est le cas, n'hésite pas à réviser ces notions à l'occasion en t'aidant des récap de cours et d'anciens challenges.

Tu as manqué de méthode et de rigueur sur ce parcours. Rassures-toi, ce sont des choses qui s'apprennent. Tu feras de gros progrès en te disciplinant un peu et en prenant les bonnes habitudes. Le reste viendra en grande partie tout seul avec la pratique. Bon courage et bonnes révisions :)