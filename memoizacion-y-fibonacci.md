
## Recursion: este algoritmo disminuye un numero N en una unidad hasta llegar a cero. 

### El coste del este algoritmo es lineal.


```
let bar = (n) => {
    if(n <= 2) return 1;
    return bar(n - 1);
}

console.log(bar(10));

```



## Algoritmo para averiguar el numero N de la serie fibonacci 
### (cada numero de fibonacci es la suma de sus dos anteriores)

```
        4
       / \
      3   2
     / \
    2   1
```

**ej:** el 4 numero fibo es 3, por qué? cada nodo toma el valor retornado por sus hojas, con lo cual el nivel inferior
2 y 1 retornan 1 cada uno (1 no puede retornar 0 por que 1 no es la suma de un cero y el dos tambien solo tiene un 1 como hoja)

-el nodo 3 es la suma de sus hojas, por lo tanto es **1+1=2**

-el nodo 2 retorna 1

-el nodo 4 es la suma de sus hojas que valen respectivamente 2 y 1 por lo tanto el nodo 4 
(que en realidad es el tercer nivel del arbol) es **2+1= 3**

>el 4 numero de la serie fibonacci es el 3  ===> 0,1,1,2,3... (se cuenta igual que en un array, desde cero)


```

let fib = (n) => {
    if(n <= 2) return 1;
    return fib(n - 1) + fib(n - 2);
}

console.log(fib(13));
//console.log(fib(50));
```


### El problema de esta solución es que si querés calcular un numero grande el costo del algoritmo es exponencial: O^n

>Literalmente si ponés n = 50 el algoritmo se empacha.

Por qué? cuantas mas llamadas recursivas aumenta el numero de nodos exponencialmente

```

let dib = (n) => {
    if(n <= 0) return;
    dib(n-1);
    dib(n-1); 
}

```

este algoritmo resta una unidad de N hasta llegar a 0, pero hacemos DOS llamadas recursivas 
con lo cual duplicamos los nodos en cada nivel.

```
         4
       /  \
      3    3
     / \  / \
    2  2 2  2
   /\ /\ /\ /\
  1 1 1 1 1 1 1
```

>El costo es exponencial.



### la solucion al problema de el costo exponencial de calcular cada nodo es con la tecnica de MEMOIZACIÓN


```
let memoDib = (n, memo = {}) => {
    if(n in memo) return memo[n]; //busca en el objeto memo si la key existe, si existe la retorna y corta la recursion
    if(n <= 1) return 0;          //hasta que n sea igual a uno sigue la resta
    memo[n] = memoDib(n - 1, memo);  //en la posicion N insertamos lo que da la funcion recursiva
   
    console.log(memo) // imprimo el objeto para ver como se va rellenando en cada recursion  
    return memo[n];
}

console.log(memoDib(10));
```

### Se puede usar la misma estrategia para resolver el de fibonacci

```
let memoFibo = (n, memo = {}) => {
    if(n in memo) return memo[n];
    if(n <= 2) return 1;
    memo[n] = memoFibo(n - 1, memo) + memoFibo(n - 2, memo);
    return memo[n];
}

console.log(memoFibo(70));
```

Ahora si se pueden poner un numero grande en el algoritmo fibo, ya que cada numero calculado se agrega en un objeto que funciona 
como diccionario o mapa de hash. Cuando el numero ya existe en el mapa la funcion retorna en el primer if y
devuelve n (el valor actual) al nivel superior. Si no existe, sigue la recursion y baja un nivel creando dos hojas.

>Hasta 70 da resultado sin errores, mas adelante ya no sé si es un problema del procesador o que pero da divergencias 
con las tablas que encontré de fibonacci.





