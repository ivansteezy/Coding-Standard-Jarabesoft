# **Coding Standard Jarabesoft.**

## **Convenciones de nombramiento.**

### ※ Archivos
- Los archivos deben ser nombrados con [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") seguido de su respectiva extensión, los nombres deben ser claros y descriptivos, por ejemplo:


    Correcto | Incorrecto
    ------------ | -------------
    InventarioTienda.ts | InvT.ts

### ※ Variables
- Las variables deben de tener nombres descriptivos teniendo una mayor prioridad la claridad del nombre que el tamaño del nombre.

- Las variables miembro se usara ```"m_"``` seguido de notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") por ejemplo:
    ```javascript
    let m_someMemberData;
    ```

- Las variables de constantes deberán usar **SCREAMING_SNAKE_CASE** por ejemplo:
    ```javascript
    const SOME_CONSTANT_VALUE = 500;
    ```
- En el caso de contar con una sola palabra, se puede omitir el ```"_"```: 
    ```javascript
    const SECONDS = 60;
    ```

- Se recomienda evitar a toda costa el uso de variables globales, en el caso de usar se debe utilizar el prefijo ```"g"``` seguido del nombre en notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") por ejemplo:
    ```javascript
    var gSomeGlobalMessage = "Hola mundo!";

    function ShowGlobalMessage()
    {
        alert(gSomeGlobalMessage);
    }
    ```

### ※ Funciones / Métodos
- Las funciones o métodos deben de tener nombres descriptivos teniendo una mayor prioridad la claridad del nombre que el tamaño del nombre.

- Al declarar una función o método se utilizará notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case"): 
    ```javascript
    function VeryImportantTask()
    {
        //...
    }
    ```

- En el caso de que una funcion reciba argumentos, estos deberan usarse con notación [*Camel Case*]("https://es.wikipedia.org/wiki/Camel_case"), el mismo caso para las variables locales de una función, por ejemplo:
    ```javascript
    function GreetUser(userName)
    {
        let greetMessage = "Hola " + userName;
        //...
    }
    ```

## **Formato de código.**
### ※ Identación
- La identación del código debe de ser de 4 espacios, Visual Studio y Visual Studio Code por defecto tienen esta identación al tabular el texto, una correcta identacion de código dberia verse tal que:

```javascript
function SomeImportantTask(isImportantValue)
{
    if(importantValue == true)
    {
        for(let step = 0; step < 5; step++)
        {
            //...
        }
    }
}
```

### ※ Cierre y apertura de llaves
- El cierre y apertura de llaves se puede presentar en dos casos:
    - Para el caso de apertura y cierre de *scope* se hará un salto de linea antes de abrir una llave.
    - En el caso de apertura y cierre de *callbacks* ó *funciones flechas o funciones anónimas* se abrirá con una llave en la misma línea en la que se declara.

```javascript
function Persona(edad)
{
    if(edad >= 18)
    {
        setInterval(function Crecer(){
            edad++;
        }, 1000)
    }
}
```
### ※ Flags
- Sí existen más de 2 variables y/o propiedades de tipo *boolean* deben ser en su lugar un *enum flag*, por ejemplo:

Incorrecto | 
-------- | 

```javascript
let isUp    = false;
let isDown  = false;
let isRight = false;
let isLeft  = true;
```

Correcto | 
-------- | 
```javascript
var Direction = 
{
    up:    1,
    down:  2,
    right: 4,
    left:  8
};
```

### ※ Funciones flecha
- Unicamente se deberá rodear la lista de parámetros con ```( )``` si existe mas de uno:

Incorrecto | 
-------- | 
```javascript
(x) => x + x;
```

- Cualquiera de estas opciones es correcta:

Correcto | 
-------- |
```javascript
x => x + x;

(x, y) => x + y;

<T>(x: T, y: T) => x === y;
```

## **Principios de diseño**
### ※ Encapsulamiento y principios de responsabilidades
#### Condicionales repetitivas y encapsulamiento lógico
Se pueden llegar a presentar situaciones en donde se tengan condicionales condemaciadas expresiones lógicas y en la mayoría de los casos se requieren de reutilizar las mismas expresiones en otras condicionantes; la regla fundamental es la utilización de funciones anónimas y predicados:

Lógica no refactorizada | 
-------- |

```javascript
boolean hasAudio = musicList.size > 0;
boolean hasVideo = videoList.size > 0;
boolean hasKaraokes = karaokeList.size > 0;

let permisos = getConfiguracion();
if(hasAudio | hasVideo | hasKaraoke)
   mostrarDashboard();
if((hasAudio | hasVideo | hasKaraoke) && permisos.isAudioEnabled)
    mostrarTabDeMusica();
```

Lógica refactorizada | 
-------- |
```javascript
//Predicados unuarios para logica generica
let hasContentPredicate = list => { return list.size > 0; }
boolean hasAudio = hasContentPredicate(musicList);
boolean hasVideo = hasContentPredicate(videoList);
boolean hasKaraokes = hasContentPredicate(karaokeslist);

//functores y lamdas/funciones anonimas para encapsular expreciones logicas
let hasAnyMedia  = () => { return hasAudio | hasVideo | hasKaraoke; }

if(hasAneMedia())
   mostrarDashboard();

if(hasAnyMedia() && permisos.isAudioEnabled)
    mostrarTabDeMusica();
```

#### Switch's Legibles:
- Cuando un bloque switch se vuelve grande, se convierte difícil de leer que es lo que hace especificamente cada caso, para casos como el mencionado se recomendará encapsular las tareas de cada caso en funciones (ya sean anónimas o definidas), es importante identificar que recursos se procesan en esos "bloques" ya que estos principalmente indican el argumento de las posibles funciones a encapsular y termina formalizando la limpieza en donde puedes leer facilmente los casos del switch e identificar que datos son los que se manejan.

Incorrecto | 
-------- | 
```javascript 
switch(value)
{
    value.A:
        arreglo.forEach(e =>{
            e.nombre = "e";
            //...
            elementList.add(e);
        });
        break;

    value.B:
        nombreUsuario = getUsuario().nombre;
        arreglo.forEach(e => {
                if(e.nombre == nombreUsuario)
                    elementList.remove(e);
        });
        break;         
}
```

Correcto | 
-------- | 
```javascript 
let Agregar()
{
    arreglo.forEach(e =>{
        e.nombre= "e";
        //...
        elementList.add(e);
    });
}

let Eliminar(nombre)
{
    arreglo.forEach(e =>{
        if(e.nombre == nombreUsuario)
            elementList.remove(e);
    });
}

switch(value)
{
    value.A:
        Agregar();
        break;
    value.B:
        Eliminar(getUsuario().nombre);
        break;         
}
```

#### Responsabilidad de una función
- Cuando una función empieza a tener demaciado código, empiezan a crecer su         número de responsabilidades, la solución es sencilla: tener en cuenta 2          responsabilidades y en base a estas responsabilidades dividir por pasos las acciones/tareas que hace la función.

#### Responsabilidades de ejecución
- Esta es la que agrupa un segmento de funciones:

```javascript
let Ejemplo()
{
    FuncionA();
    FuncionB();
    FuncionC(FuncionD());
}
```

#### Responsabilidades de proceso
- Esta es la que se encarga de elaborar una acción pertinente.
```javascript
let FuncionA()
{
    //realiza un paso de la funcion ejemplo
}
```

- La responsabilidad de una función encamina al concepto de que tan "abierto/desacoplado" o "cerrado/acoplado" sea el codigo. Para "abrir/desacoplar" código, es importante identificar los recursos que se manejan, ya que estos son la entrada de las funciones que tienen responsabilidades tipo proceso.


# *TO DO...*


