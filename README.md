[Utilisation des promesses](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Using_promises)


### 1 - Etats d'une promesse

Une Promise est dans un de ces états :

    pending (en attente) : état initial, la promesse n'est ni tenue, ni rompue.

    fulfilled (tenue) : l'opération a réussi.

    rejected (rompue) : l'opération a échoué.



### 2 - Construteur Promise

Prend un argument une fonction executor.
Celle est composée de deux paramètres qui sont des fonctions, que l'on peut appeller à la résolution ou à l'échec.

```
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

```
maPromesse
  .then(gestionnaireSuccesA, gestionnaireEchecA)
  .then(gestionnaireSuccesB, gestionnaireEchecB)
  .then(gestionnaireSuccesC, gestionnaireEchecC);
```

Généralement mieux vaut laisser la gestion de l'erreur jusq'au .catch() final. Un appel à .catch() peut être vu comme un .then() qui n'a qu'une fonction de rappel pour gérer les cas d'échec.

```
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

```
console.log(Promise.resolve(2)) // Promesse synchrone

console.log(1)
```

### 6 - async & await

L'expression await interrompt l'exécution d'une fonction asynchrone et attend la résolution d'une promesse.

Lorsque la promesse est résolue (tenue ou rompue), la valeur est renvoyée et l'exécution de la fonction asynchrone reprend.

Si la valeur de l'expression n'est pas une promesse, elle est convertie en une promesse résolue ayant cette valeur.

S'utilise dans une fonction async

```
async function asyncFunc() {
  let res = await httpReq();
  // Poursuite de l'execution
}
```

Une fonction async retourne toujours une promesse

```
async function asyncFunc() {
  return 'chaine de charactère traduit en promesse';
}
```

Gestion des erreurs (via trycatch)

```
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

```
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