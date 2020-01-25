# **Coding Standard Jarabesoft v1.0.0.**

### ※ Archivos
- Los archivos deben ser nombrados con [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") seguido de su respectiva extensión, los nombres deben ser claros y descriptivos, por ejemplo:


    Correcto | Incorrecto
    ------------ | -------------
    StoreInventory.ts | StrInv.ts

### ※ Variables
- Las variables deben de tener nombres descriptivos teniendo una mayor prioridad la claridad del nombre que el tamaño del nombre.

- Entre más uso tenga una variable, más descriptivo deberá ser su nombre, por ejemplo:
    ```javascript
    for (const item of myCollection) {
        //do some stuff...
    }
    ```
    Es aceptable puesto a que ``` item ``` unicamente existirá dentro del [Scope](https://es.wikipedia.org/wiki/%C3%81mbito_(programaci%C3%B3n)) del bucle.

- Por lo que:

    ```javascript
        let usersInLocalDatabase = { 
            /* .. */
        }
    ```
    Es aceptable, puesto que es una variable que posiblemente será usada en más de un lugar.

- Las variables de constantes deberán usar **SCREAMING_SNAKE_CASE** por ejemplo:
    ```javascript
    const SOME_CONSTANT_VALUE = 500;
    ```
- En el caso de contar con una sola palabra, se puede omitir el ```"_"```: 
    ```javascript
    const SECONDS = 60;
    ```

- Para el uso de variables ```boolean``` se recomiendan los sufijos *is* o *has*.

- Se recomienda evitar a toda costa el uso de variables globales, en el caso de usar se debe utilizar el prefijo ```"global"``` seguido del nombre en notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") por ejemplo:
    ```javascript
    var globalGreetMessage = "Hola mundo!";

    function ShowGlobalMessage()
    {
        alert(globalGreetMessage);
    }
    ```

### ※ Funciones / Métodos
- Las funciones o métodos deben de tener nombres descriptivos teniendo una mayor prioridad la claridad del nombre que el tamaño del nombre.

- Los nombres de las funciones deben ser entendidas como acciones.

- El nombre de una función debe entenderse como una acción.

- Al declarar una función o método se utilizará notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case"): 
    ```javascript
    function DoVeryImportantTask()
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

### ※ Idioma
- Todas las convenciones anteriormente mencionadas debes hacer uso del idioma **Inglés** sin ninguna excepción.

## **Formato de código.**
### ※ Identación
- La identación del código debe de ser de 4 espacios, Visual Studio y Visual Studio Code por defecto tienen esta identación al tabular el texto, una correcta identacion de código dberia verse tal que:

```javascript
function DoSomeImportantTask(isImportantValue)
{
    if(isImportantValue == true)
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
function GetAge(edad)
{
    if(age >= 18)
    {
        setInterval(function Grow(){
            age++;
        }, 1000)
    }
}
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
```

## **Principios de diseño**
### ※ TDD (Test-driven development)
[TDD ó desarrollo guiado por pruebas](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas) es una técnica de desarrollo de software que se base en primero realizar pruebas y [*refactoring*](https://es.wikipedia.org/wiki/Refactorizaci%C3%B3n).

![](https://robertonovacid.files.wordpress.com/2014/01/tdd_flow.gif?w=293&h=307)

**Los pasos a seguir son:**
- **Elegir un requisito ó requerimiento:** Se elige de una lista el requerimiento que se cree que nos dará mayor conocimiento del problema y que a la vez sea fácilmente implementable.

- **Escribir una prueba:** Se comienza escribiendo una prueba para el requisito.

- **Verificar que la prueba falla:** Si la prueba no falla es porque el requerimiento ya estaba implementado o porque la prueba es errónea.

- **Escribir la implementación:** Escribir el código más sencillo que haga que la prueba funcione.

- **Ejecutar las pruebas:** Verificar si todo el conjunto de pruebas funciona correctamente.

- **Eliminación de duplicación:** El paso final es la refactorización, que se utilizara principalmente para eliminar código duplicado.

- **Actualización de la lista de requisitos:** Se actualiza la lista de requisitos tachando el requisito implementado. Asimismo se agregan requisitos que se hayan visto como necesarios durante este ciclo y se agregan requerimientos de diseño.


### ※ Encapsulamiento y principios de responsabilidades
#### Condicionales repetitivas y encapsulamiento lógico
Se pueden llegar a presentar situaciones en donde se tengan condicionales condemaciadas expresiones lógicas y en la mayoría de los casos se requieren de reutilizar las mismas expresiones en otras condicionantes; la regla fundamental es la utilización de funciones anónimas y predicados:

Lógica no refactorizada | 
-------- |

```javascript
boolean hasAudio = musicList.size > 0;
boolean hasVideo = videoList.size > 0;
boolean hasKaraokes = karaokeList.size > 0;

let configurations = getConfigurations();
if(hasAudio | hasVideo | hasKaraoke)
   ShowDashBoards();
   
if((hasAudio | hasVideo | hasKaraoke) && configurations.isAudioEnabled)
    ShowMusicTab();
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

## **※ Bases de datos**

#### Relaciones
- Una relación es una característica especial de Acceso que hace que podamos trabajar con varias tablas relacionadas a través de un campo en común.

#### Relación de uno a uno:
-Las relaciones de uno a uno no son las más habituales, y de hecho muchas veces se evitan, pero tenemos ejemplos típicos que se repiten en diferentes aplicaciones: por ejemplo, un proovedor tiene una cuenta.

![Relacion uno a uno](https://loopback.io/pages/en/lb4/imgs/hasOne-relation-example.png)

#### Relación de uno a muchos:
-Una relación uno a muchos es utilizada cuando un modelo puede tener muchos otros modelos relacionados. Por ejemplo, una profesión puede tener un número indeterminado de usuarios asociados a ésta. Dentro del modelo Profession podemos decir que una profesión tiene muchos usuarios:

![Relación de uno a muchos](https://loopback.io/pages/en/lb4/imgs/hasMany-relation-example.png)

#### Relación de HasManyThrough :
-En las relaciones HasManyThrough tenemos una relación a través de otra tabla, desde el modelo de Physician hacia el de Pacient. Estos dos modelos no se encuentran relacionados directamente entre sí, pero sin embargo sí que es posible llegar desde los cursos a los recursos, a través de la tabla de Appointment.

![Relación de HasManyThrough](https://loopback.io/images/9830482.png)

#### Relación de HasAndBelongsToMany :
-En las relaciones HasAndBelongsToMany crea una relacion muchos a muchos directa con otro modelo sin necesidad de una tabla intermedia a comparacion de HasManyThrough . Por ejemplo, en una aplicacion con ensamble y partes, donde cada ensamble tiene muchas partes en varios ensambles.

![Relación HasAndBelongsToMany](https://loopback.io/images/9830483.png)


#### Extensión del código
- El cuerpo de una funcion no deberá de sobrepasar las 20 líneas de código.

- Un archivo no deberá de sobrepasar las 300 líneas de código.

## ※ Distribución correcta de los archivos.

- Las funciones deben estar correctamente distribuidas en sus respectivos archivos, un ejemplo de una mala práctica sería tener la validación / encriptación de los datos del usuario en el mismo archivo en el que se recolectan dichos datos, lo correcto sería tener separados ambos modulos y así:
    
    - Se reutiliza código.
    - Es más fácil de leer.
    - Es más fácil de reparar.

## ※ Commits.

- Al igual que las convenciones de nombramiento antes mostradas, los commits deben de ser claros y explicitos respecto a los cambios que se hicieron (desarrollo de un feature nuevo, reparación de un bug, refactor de alguna sección, etc), para de esta manera detectar errores más rápido.