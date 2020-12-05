## Algoritmo canSum

Este problema es sobre comprobar si se puede obtener un numero dado con la suma de un numero indeterminado 
de los elementos de un array, ¿como es la historia? si el numero objetivo es 4 y te dan un array con [2,1,5]
el algoritmo retorna true porque podes sumar dos veces 2 y llega a 4.

```
const canSum = (targetSum, numbers) => {
    if (targetSum === 0) return true; //el caso base, si n llega a cero retorna true
    if (targetSum < 0) return false; //en caso que el ciclo de restas retorne un valor negativo (nos pasamos de largo) retorna falso

    for(let num of numbers){ //iteramos el array de numeros a comprobar (atento al OF y no IN del FOR)
        
        const remainder = targetSum - num; //realizamos la resta del numero por un elemento del array
        if(canSum(remainder, numbers) === true) { //chequeamos bajando un nivel pero pasando el resto del numero inicial
            return true; //si devuelve la recursion true, retornamos true
        }
        
    }
    return false; //si salimos del bucle y no saltó el true, es porque es falso que una suma de dos elementos del array de el numero base
}

//console.log(canSum(7, [2,3,5,9,1]));
//console.log(canSum(5, [9,1]));
console.log(canSum(7, [2,3]));
console.log(canSum(4, [2,1,5]));
console.log(canSum(7, [2,4]));

```

## Version memoizada

>es lo mismo pero agregando el objeto en la funcion

```
const canSumMemo = (targetSum, numbers, memo = {}) => {
    if(targetSum in memo) return memo[targetSum]; //con esto hacemos el fetch(busqueda) en el objeto de cada resultado de la resta

    if (targetSum === 0) return true; //el caso base, si n llega a cero retorna true
    if (targetSum < 0) return false; //en caso que el ciclo de restas retorne un valor negativo (nos pasamos de largo) retorna falso

    for(let num of numbers){ //iteramos el array de numeros a comprobar (atento al OF y no IN del FOR)
        
        const remainder = targetSum - num; //realizamos la resta del numero por un elemento del array
        if(canSumMemo(remainder, numbers, memo) === true) { //chequeamos bajando un nivel pero pasando el resto del numero inicial
            memo[targetSum] = true; //con esto ingresamos en valor a la key actual del objeto
            console.log(memo);
            return true; //si devuelve la recursion true, retornamos true
        }
        
    }
    memo[targetSum] = false; //con esto ingresamos false como valor de la key actual del objeto
    console.log(memo);
    return false; //si salimos del bucle y no saltó el true, es porque es falso que una suma de dos elementos del array de el numero base
    
}

console.log(canSumMemo(14, [4,5]));
console.log(canSumMemo(300, [7,14]));
```

Ahora podemos poner entradas mas grandes y el arbol no empacha a la maquina

