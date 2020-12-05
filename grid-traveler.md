

## Grid traveler

>La idea es calcular cuantas rutas podemos tener para recorrer una grilla NxM si empezamos en la esquina superior
>izquierda y solo podemos movernos hacia abajo y hacia la derecha y tenemos que llegar a la esquina inferior derecha.

>






```
const gridTraveler = (m, n) => {
    if(m == 1 && n == 1) return 1; //si llagemos a una hoja (1,1) se retorna 1 (true)
    if(m == 0 || n == 0) return 0; //si llegamos a una hoja con uno de los terminos en cero, retornamos cero (esta fuera del tablero)
    return gridTraveler(m - 1, n) + gridTraveler(m, n - 1); //suma el resultadod e cada hoja hacia arriba, llegando al root
}

console.log(gridTraveler(3, 2)); //la salida de la funcion es la cantidad de rutas para llegar a el destino. 
console.log(gridTraveler(6, 6));      
```



Esto fue una solución de fuerza bruta, como el primer algoritmo de fibonacci. Si le metés un numero grande de grilla nxn
se te va a empachar.


## Version memoizada

```
const gridTravelerMemo = (m, n, memo = {}) => {
    let key = m + ',' + n;
    if(key in memo) return memo[key]; //revisamos si el nodo ya está en el objeto
    if(m === 1 && n === 1) return 1; //si llagemos a una hoja (1,1) se retorna 1 (true)
    if(m === 0 || n === 0) return 0; //si llegamos a una hoja con uno de los terminos en cero, retornamos cero (esta fuera del tablero)
    memo[key] = gridTravelerMemo(m - 1, n, memo) + gridTravelerMemo(m, n - 1, memo); //suma el resultado de cada hoja hacia arriba, llegando al root
    return memo[key];
}

console.log(gridTravelerMemo(18, 18));

```

## Receta general

- visualizar el problema como un arbol.
- implementar un arbol recursivo.
- probar que un imput grande no lo empache.
- agregar un objeto vacio en el tope del arbol recursivo
- definir casos base
- ingresar el nodo en el objeto


