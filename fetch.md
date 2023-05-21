# Conseil technique : méthode fetch

Salut Apprenant,

A ta demande, je vais tâcher de t'expliquer un peu la méthode fetch de javascript : qu'est ce que c'est, à quoi ça sert, comment l'utiliser.
Pour ne pas trop m'épancher, je ne rentrerai pas dans le détail de certaines notions annexes ou plus avancées qui sont liées à fetch. J'essaierai toutefois de te laisser des liens vers la documentation pour ces choses que je laisse de côté.

Je t'encourage a tester et expérimenter avec les morceaux de codes que je vais te montrer pour te faire ton propre ressenti de la chose.

## Qu'est ce que fetch

Fetch est une méthode de JavaScript permettant d'effectuer des requêtes HTTP. En gros, son utilité est d'échanger des informations avec un serveur.
Tu verras dans des projets plus avancés et notamment pendant l'apothéose que c'est souvent ce qu'on utilise pour faire des requêtes au back depuis le front.

La méthode fetch a deux paramètre. Le premier sera typiquement l'URL à laquelle on souhaite effectuer la requête.

Le second doit être un objet pouvant définir tout un tas d'options. Je ne veux pas trop t'embrouiller avec ce second paramètre, mais retiens que c'est là que tu vas pouvoir définir quel méthode HTTP utiliser (GET, POST, DELETE, etc.) et quel contenu envoyer avec la requête le cas échéant. Il y a des exemples d'utilisation de ce paramètre dans [la documentation de fetch sur MDN](https://developer.mozilla.org/fr/docs/Web/API/fetch) si tu souhaites approfondir.

Pour l'exemple on va effectuer toujours la même requête sur l'adresse de ton serveur ou on récupère la liste des posts. On va omettre le second paramètre, car par défaut la méthode employée est GET. Voilà à quoi ça devrait ressembler :

```js
const response = fetch('https://monserveur.fr/posts');
```

## Asynchrone et Promise

Si tu testes le code ci-dessus en y ajoutant `console.log(response)` à la ligne suivante, tu verras dans la console apparaître un objet `Promise` avec l'état `pending`.

Pour l'expliquer, je dois rapidemment expliquer les promesses et l'asynchonicité dans JavaScript. Lorsqu'un script JS tourne, il s'exécute ligne par ligne dans l'ordre d'écriture. C'est embêtant puisque lorsqu'on a une tâche un peu longue à effectuer, typiquement une requête HTTP dont la réponse prend un certain temps à arriver, le script continue à s'exécuter sans attendre que la tâche soit résolue. C'est exactement ce qu'il se passe dans notre exemple, où le `console.log(response)` s'est exécuté avant que la réponse du serveur n'ait été reçue.

C'est pour gérer ce genre de cas que JS mets à disposition une classe `Promise`, une promesse, qui est le type d'objet renvoyé par `fetch()`. Une `Promise` peut être `pending` (en cours), `fulfilled` (tenue avec succès) ou `rejected` (rejetée). JS nous a indiqué qu'au moment du `console.log(response)` la promesse était encore en cours.

Il existe deux méthode permettant de traiter le résultat d'une promesse tenue, que je vais maintenant te présenter.

## Promise.then()

Tout d'abord il y a `Promise.then()`, qui permet de traiter une `Promise` une fois que celle-ci est tenue. Pour utiliser cette méthode, il faut lui donner en argument une callback, autrement dit une fonction qui va s'exécuter sur la promesse tenue.
Voilà comment on peut modifier le code précédent pour exécuter la requête puis afficher le résultat renvoyé par le serveur sous forme JSON dans la console :

```js
fetch('https://monserveur.fr/posts')
    .then((response) => {
        return response.json();
    })
    .then((posts) => {
        console.log(posts);
    });
```

Tu relèveras sûrement le fait que j'ai utilisé deux fois de suite `.then()`. C'est nécessaire car [la méthode `.json()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/json) retourne elle même une promesse. Il me faut donc un second `.then()` pour traiter celle-ci une fois tenue.

C'est très courant de devoir enchaîner les `.then()` et parfois difficile de savoir quand on en a besoin. Mon bon conseil, c'est de tester ton code avec des `console.log()`, et si tu vois que tu as encore une promesse à traiter, alors il te faut ajouter un `.then()`. L'instinct de la chose finira par venir avec la pratique.

## async function

L'autre méthode provient d'une évolution de JS plus récente : les fonctions asynchrones. Pour créer une fonction asynchrone, il suffit d'ajouter le mot clé `async` devant sa déclaration.

L'utilité d'une fonction asynchrone, c'est qu'elle autorise l'utilisation du mot clé `await` à l'intérieur de la fonction, qui permet d'attendre la résolution de la promesse !
Si on reprend notre exemple, mais avec la syntaxe async/await, cela donne le code suivant :

```js
async function getPosts() {
    const response = await fetch('https://monserveur.fr/posts');
    const posts = await response.json();
    console.log(posts);
};

getPosts();
```

Cette syntaxe ressemble beaucoup plus à ce dont on a l'habitude quand on apprend JavaScript.
On peut faire la même remarque qu'avec l'exemple précédent : j'ai eu besoin d'utiliser await deux fois `await`, d'abord pour attendre la réponse du serveur, puis pour attendre la conversion en JSON. Même conseil, n'hésite pas à tester à coup de `console.log()` et d'ajouter un `await` là où tu trouves une promesse en cours.

## Conclusion

Voilà pour l'explication de `fetch()` et des deux syntaxes. J'espère avoir été clair et pas trop long !

Personnellement, j'ai une préférence pour l'utilisation des fonctions asynchrones car je trouve cette syntaxe un peu plus digeste et parce qu'elle offre un peu plus de liberté car on est pas obligé d'enchaîner les `.then()` successifs.
Par contre c'est quand même bien de connaître les deux syntaxes, car `.then()` est toujours très utilisé.

Si tu veux approfondir un peu tout ça je te conseille de regarder comment utiliser [le second paramètre de `fetch()`](https://developer.mozilla.org/fr/docs/Web/API/fetch), notamment pour faire des requêtes avec la méthode HTTP POST.

Si tu veux aller encore plus loin, tu peux regarder comment faire de la gestion d'erreur autour des requêtes et réponses. Pour ça, renseigne-toi sur [la classe `Error`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Error), et [la méthode `Promise.catch()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) dont la syntaxe est proche de celle de `.then()`.
