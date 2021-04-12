# Coding Standard

## Tabla de contenidos
El aspecto mas importante del estilo es la _consistencia_, si todes nos regimos bajo un mismo estándar de código y todes nos acostumbramos a el, leerlo, manternelo y cambiarlo será mucho más fácil.

Por lo que es importante apegarse de una manera casi _religiosa_ al estilo especificado.

### ※ Archivos
- Los archivos generados manualmente deben ser nombrados con [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") seguido de su respectiva extensión, los nombres deben ser claros y descriptivos, por ejemplo:


    Correcto | Incorrecto
    ------------ | -------------
    StoreInventory.ts | StrInv.ts

- En el caso de utilizar los frameworks del stack actual (Angular, Loopback y Ionic) los archivos generados deberán respetan el nombramiento default. 

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

- Para el uso de variables ```boolean``` se recomiendan los sufijos *is* o *has*.

- Se recomienda evitar a toda costa el uso de variables globales, en el caso de usar se debe utilizar el prefijo ```"global"``` seguido del nombre en notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case") por ejemplo:
    ```javascript
    var globalGreetMessage = "Hola mundo!";

    function ShowGlobalMessage()
    {
        alert(globalGreetMessage);
    }
    ```

#### Nombramiento

### ※ Funciones / Métodos
- Las funciones o métodos deben de tener nombres descriptivos teniendo una mayor prioridad la claridad del nombre que el tamaño del nombre.

- El nombre de una función debe entenderse como una acción.

- Al declarar una función o método se utilizará notación [*Pascal Case ó Upper Camel Case*]("https://es.wikipedia.org/wiki/Camel_case"): 
    ```javascript
    function DoVeryImportantTask()
    {
        //...
    }
    ```

- En el caso de que una función reciba argumentos, estos deberan usarse con notación [*Camel Case*]("https://es.wikipedia.org/wiki/Camel_case"), el mismo caso para las variables locales de una función, por ejemplo:
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
- La identación del código debe de ser de 2 espacios, Visual Studio Code por defecto tienen esta identación al tabular el texto, una correcta identacion de código debería verse tal que:

```javascript
function DoSomeImportantTask(isImportantValue) {
  if(isImportantValue == true) {
    for(let step = 0; step < 5; step++) {
          //...
    }
  }
}
```

### ※ Uso de llaves y paréntesis.
Existen [muchos estilos del uso llaves e identación](https://en.wikipedia.org/wiki/Indentation_style) en Jarabe esta adoptada el estilo _K&R_ el cual es una variante del _One True Brace Style_, tiene la siguiente forma: 

```typescript
enum Color {
    Red,
    Orange,
    Yellow,
    Green,
    Blue,
    Purple
};

function MaxValue(number1: number, number2: number) {
  if (number1 > number2) {
      return number1;
  } else {
      return number2;
  }
}
```
La identación es a **dos espacios**, las sentencias _else_ se colocan en la línea que cierra la sentencia _if_, esto con el fin de que al insertar codigo dentro de este bloque, no se rompa la estructura.

## ※ Strings
### Single quotes vs Double quotes
Use _single quotes_ `('')` para las _strings_, cada vez más equipos que utilizan Javascript/Typescript (por ejemplo, _Airbnb_, _Angular_ o _Npm_) han adoptado esta práctica, aparte de que es más fácil de escribir (no es necesario precionar shift en la mayoria de los teclados).

```javascript
// mal :(
const companyName = "JarabeSoft";

// mal, plantillas de cadena deben tener concatenación o interpolación
const companyName = `JarabeSoft`;

// bien <3
const companyName = 'JarabeSoft';
```

### Template strings
Cuando se vaya a construir cadenas de manera _no-manual_, use [plantillas literales](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Template_literals)

```javascript
// mal :(
function SayGoodMorning(name) {
    return 'Good morning, ' + name + '!';
}

// bien <3
function SayGoodMorning(name) {
    return `Good morning, ${name} !';
}
```
### ※ Funciones anónimas
- Cuando se utilicen funciones anónimas (por ejemplo, cuando se pasa un _callback_ _inline_), use una función flecha.

```javascript
// mal :(
[1, 2, 3].map(function (item) {
  const res = item + 1;
  return res * item;
});

// bien <3
[1, 2, 3].map((item) => {
  const res = item + 1;
  return res * item;
});
```

Esto puesto a que con una función flecha se crea una version que se ejecuta in el contexto de _this_, que es lo que muuuy probablemente necesites aparte de que es una sintaxis más conciso.


#### Estilos
- Para identificar una clase CSS esta deberá estar escrita en kebab-case, ejemplo: bg-dark, cursor-pointer, text-center.

- Los identificadores HTML serán nombrados en PascalCase.

- Los estilos se aplicarán únicamente mediante clases e identificadores, prohibiendo el uso del atributo "style" en los elementos HTML.


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
Se pueden llegar a presentar situaciones en donde se tengan condicionales con demaciadas expresiones lógicas y en la mayoría de los casos se requieren de reutilizar las mismas expresiones en otras condicionantes; la regla fundamental es la utilización de funciones anónimas y predicados:

Lógica no refactorizada | 
-------- |

```javascript
const RefreshUI()
{
    boolean hasAudio = musicList.size > 0;
    boolean hasVideo = videoList.size > 0;
    boolean hasKaraokes = karaokeList.size > 0;

    let configurations = getConfigurations();
    if(hasAudio | hasVideo | hasKaraoke)
        ShowDashBoards();

    if((hasAudio | hasVideo | hasKaraoke) && configurations.isAudioEnabled)
        ShowMusicTab();
}
```

Lógica refactorizada | 
-------- |
```javascript
const RefreshUI()
{
    //Predicados usuarios para lógica generica
    let hasContentPredicate = list => { return list.size > 0; }
    boolean hasAudio = hasContentPredicate(musicList);
    boolean hasVideo = hasContentPredicate(videoList);
    boolean hasKaraokes = hasContentPredicate(karaokeslist);

    //functores y lamdas/funciones anónimas para encapsular expreciones lógicas
    let hasAnyMediaType  = () => { return hasAudio | hasVideo | hasKaraoke; }
    
    let configurations = getConfigurations();  
      
    if(hasAnyMediaType())
       ShowDashBoards();

    if(hasAnyMediaType() && configurations.isAudioEnabled)
        ShowMusicTab();
}
```

#### Switch's Legibles:
- Cuando un bloque switch se vuelve grande, se convierte difícil de leer que es lo que hace especificamente cada caso, para casos como el mencionado se recomendará encapsular las tareas de cada caso en funciones (ya sean anónimas o definidas), es importante identificar que recursos se procesan en esos "bloques" ya que estos principalmente indican el argumento de las posibles funciones a encapsular y termina formalizando la limpieza en donde puedes leer facilmente los casos del switch e identificar que datos son los que se manejan.

Incorrecto | 
-------- | 
```javascript 
...
switch(value)
{
    case 'AddUserCase':
        let recentlyCreatedUser = {name,pass,email,rights};
        recentlyCreatedUser.name = "example";
        //... some magical stuff inbetwen
        elementList.add(recentlyCreatedUser);
        break;

    case 'DeleteUser':
        someArray.forEach(e =>{
            if(e.name == selectedUser.name)
                someArray.remove(e);
            });
        break;         
}
...
```

Correcto | 
-------- | 
```javascript 
...
let AddUser(elementList)
{
    let recentlyCreatedUser = {name,pass,email,rights};
    recentlyCreatedUser.name = "example";
    //... some magical stuff inbetwen
    elementList.add(recentlyCreatedUser);
}

let DeleteUser(someArray,userName)
{
    someArray.forEach(e =>{
        if(e.name == userName)
            someArray.remove(e);
    });
}

...
switch(value)
{
    case 'AddUser':
        AddUser(elementList);
        break;
    case 'DeleteUser':
        DeleteUser(elementList,selectedUser.name);
        break;         
}
...
//IMPORTANT NOTE: THIS CODE IS JUST AN EXAMPLE;VAR DECLARATIONS AND THE STRUCTURE OF THE GENERAL IDEA TO REPRESENT ARE UNDER THE HOOD;
```

#### Responsabilidad de una función
- Cuando una función empieza a tener gran cantidad de código,  su número de responsabilidades incrementa, la solución es sencilla: tener en cuenta 2 responsabilidades y en base a estas responsabilidades dividir por pasos las acciones/tareas que hace la función.

#### Responsabilidades de ejecución
- Esta es la que agrupa un segmento de funciones:

```javascript
const Example()
{
    FunctionA();
    FunctionB();
    FunctionC(FunctionD(),data.imageBuffer);
}
```

#### Responsabilidades de proceso
- Esta es la que se encarga de elaborar una acción pertinente.
```javascript
const FunctionD(inputValue,imageData)
{
    //do some bussines logic
}
```

- La responsabilidad de una función encamina al concepto de que tan "abierto/desacoplado" o "cerrado/acoplado" sea el codigo. Para "abrir/desacoplar" código, es importante identificar los recursos que se manejan, ya que estos son la entrada de las funciones que tienen responsabilidades tipo proceso.


## **※ Bases de datos**

#### Relaciones
- Una relación es una característica especial de Acceso que hace que podamos trabajar con varias tablas relacionadas a través de un campo en común.

- El nombre de la foreign key estará designado por "[propiedad] + Id", escrita en camelCase, ejemplo : storeId, storeProductId

#### Relación de uno a uno:
- Las relaciones de uno a uno no son las más habituales, y de hecho muchas veces se evitan, pero tenemos ejemplos típicos que se repiten en diferentes aplicaciones: por ejemplo, un proovedor tiene una cuenta.

![Relacion uno a uno](https://loopback.io/pages/en/lb4/imgs/hasOne-relation-example.png)

#### Relación de uno a muchos:
- Una relación uno a muchos es utilizada cuando un modelo puede tener muchos otros modelos relacionados. Por ejemplo, una profesión puede tener un número indeterminado de usuarios asociados a ésta. Dentro del modelo Profession podemos decir que una profesión tiene muchos usuarios:

![Relación de uno a muchos](https://loopback.io/pages/en/lb4/imgs/hasMany-relation-example.png)

#### Relación de HasManyThrough :
- En las relaciones HasManyThrough tenemos una relación a través de otra tabla, desde el modelo de Physician hacia el de Pacient. Estos dos modelos no se encuentran relacionados directamente entre sí, pero sin embargo sí que es posible llegar desde los cursos a los recursos, a través de la tabla de Appointment.

![Relación de HasManyThrough](https://loopback.io/images/9830482.png)

#### Relación de HasAndBelongsToMany :
- En las relaciones HasAndBelongsToMany crea una relacion muchos a muchos directa con otro modelo sin necesidad de una tabla intermedia a comparacion de HasManyThrough . Por ejemplo, en una aplicacion con ensamble y partes, donde cada ensamble tiene muchas partes en varios ensambles.

![Relación HasAndBelongsToMany](https://loopback.io/images/9830483.png)

#### Modelos :
- El nombré del modelo deberá estar escrito en singular y en PascalCase,

    Correcto | Incorrecto
    ------------ | -------------
    StoreProduct | Storeproduct
    Store        | Stores
    			    

- El modelo deberá contener sus respectivos ACL's para el control de acceso.

#### API Path - Principios REST

- Utilizar los principios REST para manejar acciones CRUD usando métodos HTTP de la siguiente forma:	

	- GET /products- Devuelve una lista de products
	- GET /products/12- Devuelve un producto específico
	- POST /products- Crea un nuevo product
	- PUT /products/12- Actualiza el producto #12
	- PATCH /products/12- Actualiza parcialmente el producto #12
	- DELETE /products/12- Elimina el producto #12

- En cuanto a relaciones se refleja de esta manera:

	- GET /products/12/messages - Devuelve una lista de mensajes para el producto #12
	- GET /products/12/messages/5 - Devuelve el mensaje #5 para el producto #12
	- POST /products/12/messages - Crea un nuevo mensaje en el producto #12
	- PUT /products/12/messages/5 – Actualiza el mensaje #5 para el producto #12
	- PATCH /products/12/messages/5 - Actualiza parcialmente el mensaje #5 para el producto #12
	- DELETE /products/12/messages/5 - Borra el mensaje #5 para el producto #12

- En caso de agregar un filtro, especificar el parámetro que se estará enviando, por ejemplo:
- GET /store/sales/12/from/2021-01-31/to/2021-02-03- Devuelve las ventas de la tienda #12 en el intervalo del 31 de enero de 2021 al 03 de febrero del 2021

Referencias:
https://api.gov.au/standards/national_api_standards/naming-conventions.html
https://restfulapi.net/resource-naming/
https://stoplight.io/blog/rest-api-standards-do-they-even-exist/

#### Extensión del código
- El cuerpo de una funcion no deberá de sobrepasar las 20 líneas de código.

- Un archivo no deberá de sobrepasar las 300 líneas de código.

## ※ Distribución correcta de los archivos.

- Las funciones deben estar correctamente distribuidas en sus respectivos archivos, un ejemplo de una mala práctica sería tener la validación / encriptación de los datos del usuario en el mismo archivo en el que se recolectan dichos datos, lo correcto sería tener separados ambos modulos y así:
    
    - Se reutiliza código.
    - Es más fácil de leer.
    - Es más fácil de reparar.

## ※ Rutas de navegación.
- Las rutas de navegación deben estar escritas en kebab-case y nombradas de forma que se pueda identificar el rol y a qué información accederá, por ejemplo:
inicio/admin/estudiantes/13/materias
En este caso, el administrador está ingresando a la información de las materias del alumno 13.