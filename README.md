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