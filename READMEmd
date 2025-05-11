### Description

En JavaScript, les tableaux ne sont pas des primitives, mais des Array objects avec les caractéristiques suivantes :

- Les tableaux sont resizable et peuvent contenir un mix de différents types

- Accessible par index

- Indéxés à partir de 0

- Les opérations de copie sont des shallow copies (utiliser les deep copies)

#
### Methodes

### Méthodes statiques

Array.from()

    Cette méthode permet de créer une nouvelle instance d'Array à partir d'un objet semblable à un tableau ou d'un itérable.
Array.isArray()

    Cette méthode renvoie true si la variable est un tableau, false sinon.
Array.of()

    Cette méthode permet de créer une nouvelle instance d'Array à partir d'un nombre variable d'arguments (peu importe la quantité ou le type des arguments utilisés).

#
### Ajout : .push() & unshift()

La méthode `push()` ajoute un ou plusieurs éléments à la fin d'un tableau et retourne la nouvelle taille du tableau.

La méthode `unshift()` ajoute un ou plusieurs éléments au début d'un tableau et renvoie la nouvelle longueur du tableau.

```javascript
arr = [...arr1, 6] // On réassigne le même tableau via le spread operator + la nouvelle valeur

arr1.splice(0, 0, "Bonjour")
```

#
### Suppression : .pop() & .shift()

La méthode `pop()` supprime le dernier élément d'un tableau et retourne cet élément. Cette méthode modifie la longueur du tableau.

La méthode `shift()` permet de retirer le premier élément d'un tableau et de renvoyer cet élément. Cette méthode modifie la longueur du tableau.

#### Autre manière de supprimer : .splice() et spread operator

```javascript
arr1.splice(-1, 1) // -1 est le dernier élément du tableau

const [, , ...copie] = arr1 // On délaisse ce qui nous intéresse pas
```

#### .splice()

La méthode `splice()` modifie le contenu d'un tableau en retirant des éléments et/ou en ajoutant de nouveaux éléments à même le tableau.On peut ainsi vider ou remplacer une partie d'un tableau.

```javascript
const months = ["Jan", "March", "April", "June"];
months.splice(1, 0, "Feb");
// Inserts at index 1

months.splice(4, 1, "May");
// Replaces 1 element at index 4
```

Premier param : L'indice à partir duquel commencer à changer le tableau

Second param : Un entier indiquant le nombre d'anciens éléments à remplacer, si 0, rien n'est supprimé

Troisième param : Valeur à ajouter

#
### .slice()

La méthode `slice()` renvoie un objet tableau, contenant une copie superficielle (shallow copy) d'une portion du tableau d'origine, la portion est définie par un indice de début et un indice de fin (exclus). Le tableau original ne sera pas modifié.

```javascript
arr.slice(); // copie sans changement
arr.slice(début);
arr.slice(début, fin);
```

#
### Méthodes renvoyant un Array iterator

#### .keys(), .values() & .entries()
Chacune des méthodes renvoie un Array Iterator

```javascript
const iterator = ["a", "b", "c"].values();

console.log(iterator.next().value) // "a"
```

#
### Trouver un élément

```javascript
arr1.find(a => typeof a == "function")

arr.findLast(a => typeof a == "function") // comme find() mais parcourt tableau dans sens inverse
```

Index d'un élément recherché (callback fn en param)
```javascript
arr1.findIndex(a => typeof a == "function")

arr.findLastIndex(a => typeof a == "function") // comme findIndex() mais parcourt tableau dans sens inverse
```

Index d'un élément recherché (valeur en param)
```javascript
arr1.indexOf("bonjour")

arr.LastIndexOf("bonsour") // comme indexOf() mais parcourt tableau dans sens inverse
```

Si oui ou non le tableau contient une valeur
```javascript
arr1.includes('bonjour')
```

#
### Fusion

#### .join()
Crée et renvoie une nouvelle chaîne de caractères en concaténant tous les éléments d'un tableau

```javascript
['b', 'g'].join() // "bg"

['b', 'g'].join("-") // "b-g"
```

#### .concat()
Renvoie la fusion deux ou plusieurs tableaux en les concaténant

```javascript
[1, 2].concat([3, 4])
```

#### spread operator

```javascript
[...[1, 2], ...[3, 4]]
```

#
### Tri

#### .sort()

```javascript
// Pour des chiffres
[1, 22, 5, 44].sort() // Attention : [1, 22, 44, 5]
[1, 22, 5, 44].sort((a, b) => a - b)

// Strings
["c", "f", "b"].sort((a, b) => a.localeCompare(b))
```

#### .reverse() & .toReversed()

La méthodes `reverse()` inverse le tableau & `toReversed()` renvoie un tableau inversé


#
### Fonctionnelle

#### .every() & .some()
permetent de vérifier une condition donnée par une fonction en argument.

```javascript
[1, 2, 33].every(nb => nb < 40) // tous doivent respecter la condition

[1, 2, 33].some(nb => nb < 4) // au moins un
```

#### .map()
Crée un nouveau tableau avec les résultats de l'appel d'une fonction fournie sur chaque élément du tableau appelant.

#### .forEach()

#### .reduce()
Applique une fonction qui est un « accumulateur » et qui traite chaque valeur d'une liste (de la gauche vers la droite) afin de la réduire à une seule valeur.

```javascript
[1, 2, 33].reduce((accumulator, currentValue) => accumulator + currentValue, 0)
```