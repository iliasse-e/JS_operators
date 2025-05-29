# Description

En JavaScript, les fonctions sont des objets de première classe. Cela signifie qu'elles peuvent être manipulées et échangées, qu'elles peuvent avoir des propriétés et des méthodes, comme tous les autres objets JavaScript. Les fonctions sont des objets Function.

#
## 1 - This & contexte d'execution

Dans JS, le this fait référence à l'objet d'éxecution.
Le this peut faire référence à différents objets en fonction du contexte dans lequel il est éxecuté.

| Type | Contexte d'execution                                                                           |
| :------------------------------------------------------- | :-------------------------------------------------------------------------------- |
| In an object method | this refers to the object.   |
| Alone | this refers to the global object. |
| In a function |this refers to the object. |
| In an arrow function |this refers to the global object. |
| In a function, in strict mode | this is undefined. |
| In an event | this refers to the element that received the event. |
| Methods like call(), apply(), and bind() | can refer this to any object. |

#
## 2 - Argument & Rest param

Rest param renvoi un tableau

```javascript
function f(a, b, ...lesArguments) {
  // ... lesArguments regroupe les param dans un tableau
}
```

`arguments` renvoie un objet avec une méthode

```javascript
function f() {
  // ... arguments regroupe chaque argument dans une propriété d'objet : {0: "arg 1", 1: "arg 2"}
}
```

#
## 3 - Environnement lexical et contexte d’exécution

JS est un langage synchrone et monothreaded

Le navigateur créé un contexte global d'execution

Dans celui ci, on a la création d'un objet Window et du this (faisant référence à ce dernier)


### Contexte d’exécution

```javascript
function a() {}

function b() { a() }

b()
```

L'éxecution du script ci dessus créé la stack (l'empilement) suivante :

#
Stack

3 | Contexte d'execution a() |

2 | Contexte d'execution b() |

1 | Objet global |
#

Dans chaque contexte d'execution on a :

- Le hoisting, qui correspond à l'initialisation des variables
- L'éxecution du code, une fois les variables créées

Une fois toutes les contextes empilés :

- Suppression du contexte, une fois l'execution terminée

### Portée et environnement lexical

```javascript
let foo = 1;

function a() {
  console.log(foo);
}

function b() {
  let foo = 2;
  a();
}

b(); // 1

```

Dans l'exemple ci dessus, la console affichera 1, car la variable foo manipulée est celle du contexte global.

```javascript
let foo = 1;

function b() {
  let foo = 2;

  function a() {
    console.log(foo);
  }
  a();
}

b(); // 2
```

Dans l'exemple ci dessus, la console affichera 2, car la variable foo manipulée est celle du contexte de la fn b().

#
## 4 - Callback fn / fonction de rappel

Une fonction de rappel (callback) est une fonction passée en argument à une autre fonction et qui est exécutée dans cette dernière. 

```javascript
setTimeout(() => console.log('Terminé'), 1000);
```
Cette fonction JavaScript native prend obligatoirement une fonction de rappel en premier argument qui sera exécutée après le temps passé en deuxième argument (qui est exprimé en millisecondes, donc 1000ms est égale à une seconde). 

#
## 5 - Closures

Une fermeture (ou closure) est une fonction qui utilise des identifiants de la portée parente, et ce même si la fonction parente n'existe plus. 