[Utilisation des promesses](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Using_promises)


### 1 - Etats d'une promesse

Une Promise est dans un de ces états :

    pending (en attente) : état initial, la promesse n'est ni tenue, ni rompue.

    fulfilled (tenue) : l'opération a réussi.

    rejected (rompue) : l'opération a échoué.



### 2 - Construteur Promise

Prend un argument une fonction executor.
Celle est composée de deux paramètres qui sont des fonctions, que l'on peut appeller à la résolution ou à l'échec.

```javascript
const promesse = new Promise((resolution, rejet) => {
  //
  //   resolution(uneValeur)    // réussite
  // ou
  //   rejet("raison d'échec")  // échec
});
```


### 3 - .then() & .catch()

Les méthodes .then() et .catch() renvoient des promesses et peuvent ainsi être chaînées. C'est ce qu'on appelle une composition.

La méthode .then() prend deux arguments : le premier est une fonction de rappel (callback) pour le cas de résolution de la promesse et le second argument est une fonction de rappel pour le cas d'échec.

```javascript
maPromesse
  .then(gestionnaireSuccesA, gestionnaireEchecA)
  .then(gestionnaireSuccesB, gestionnaireEchecB)
  .then(gestionnaireSuccesC, gestionnaireEchecC);
```

Généralement mieux vaut laisser la gestion de l'erreur jusq'au .catch() final. Un appel à .catch() peut être vu comme un .then() qui n'a qu'une fonction de rappel pour gérer les cas d'échec.

```javascript
maPromesse
  .then(gestionnaireSuccesA)
  .then(gestionnaireSuccesB)
  .then(gestionnaireSuccesC)
  .catch(gestionnaireToutEchec);
```

.then() permet de récupérer valeur d'une promesse.
.catch() permet de récupérer la raison de l'échec.


### 4 - .finally()

Permet d'exécuter du code une fois que la promesse a été traitée, quel que soit le résultat. 
On l'utiliser afin d'éviter de dupliquer du code entre les gestionnaires then() et catch().


### 5 - Synchronisation

Dans ce schéma, le log affichera : 1 puis 2

```javascript
console.log(Promise.resolve(2)) // Promesse synchrone

console.log(1)
```

### 6 - async & await

L'expression await interrompt l'exécution d'une fonction asynchrone et attend la résolution d'une promesse.

Lorsque la promesse est résolue (tenue ou rompue), la valeur est renvoyée et l'exécution de la fonction asynchrone reprend.

Si la valeur de l'expression n'est pas une promesse, elle est convertie en une promesse résolue ayant cette valeur.

S'utilise dans une fonction async

```javascript
async function asyncFunc() {
  let res = await httpReq();
  // Poursuite de l'execution
}
```

Une fonction async retourne toujours une promesse

```javascript
async function asyncFunc() {
  return 'chaine de charactère traduit en promesse';
}
```

Gestion des erreurs (via trycatch)

```javascript
async function asyncFunc() {
  try {
    let res = await httpReq();
    // suite de l'execution
  }
  catch(e) {
    throw e;
  }
}
```

### 7 - Methodes statiques

#### Promise.all()

Renvoie une promesse (Promise) qui est résolue lorsque l'ensemble des promesses contenues dans l'itérable passé en argument ont été résolues ou qui échoue avec la raison de la première promesse qui échoue au sein de l'itérable.

Prend en argument un tableau de promesses.



En cas de résolution (toutes les promesses tenues) :

```javascript
Promise.all([
  Promise.resolve(3),
  42,
  new Promise((resolve, reject) => {
    setTimeout(resolve, 100, "foo");
  });
  ]).then((values) => {
  console.log(values);
});
// Expected output: Array [3, 42, "foo"]
```

En cas d'échec (une promesse est rompue) :

```javascript
Promise.all([
  Promise.resolve(3),
  42,
  new Promise((resolve, reject) => {
    setTimeout(reject, 100, "reject");
  });
  ]).then((values) => {
  console.log(values);
});
// Expected output: "reject"
```

### Promise.allSettled()

La méthode Promise.allSettled() renvoie une promesse qui est résolue une fois que l'ensemble des promesses de l'itérable passée en argument sont réussies ou rejetées. La valeur de résolution de cette promesse est un tableau d'objets dont chacun est le résultat de chaque promesse de l'itérable.

On ne va pas dans le .catch()

Retour :

```javascript
// Tableau d'objets de cette structure :

[
  { status: "fulfilled", value: "valeur de la promesse" },
  { status: "rejected", reason: "error reason" }
]
```


### Promise.any()

La méthode Promise.any() prend comme argument un itérable contenant des objets Promise et, dès qu'une des promesses de cet itérable est tenue, renvoie une unique promesse résolue avec la valeur de la promesse résolue. Si aucune promesse de l'itérable n'est tenue (c'est-à-dire si toutes les promesses sont rejetées), la promesse renvoyée est rompue avec un objet AggregateError (une nouvelle sous-classe de Error qui regroupe un ensemble d'erreurs). Cette méthode fait essentiellement le contraire de Promise.all() (qui renvoie une promesse tenue uniquement si toutes les promesses de l'itérable passé en argument ont été tenues).


### Promise.race()

La méthode Promise.race() renvoie une promesse qui est résolue ou rejetée dès qu'une des promesses de l'itérable passé en argument est résolue ou rejetée. La valeur (dans le cas de la résolution) ou la raison (dans le cas d'un échec) utilisée est celle de la promesse de l'itérable qui est resolue/qui échoue.

### Promise.try()

Promise.try() prend une callback of any kind (returns or throws, synchronously or asynchronously) et encapsule le résultat dans une promesse.

```javascript
Promise.try(() => 'value');

Promise.try(() => { throw Error() });
```

### Promise.withResolvers()

Promise.withResolvers() retourne un objet contenant une nouvelle promesse et deux function pour tenir ou rejeter la promesse, correspondant aux deux paramètres de l'executeur de la Promise() constructor.


```javascript
 const promiseWithResolvers = Promise.withResolvers();

 // { promise: Promise { "pending" }, resolve: (), reject: () }


```
