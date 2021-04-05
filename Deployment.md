

# ※ Configurar los enviroments

Dentro de **_mobile/enviorments/_** hay 3 archivos: **_enviroment.prod.ts_**, **_enviroment.staging.ts_** y **_enviroment.ts_**, donde hay una constante donde se puede colocar la _base URL_:

```js
 export const environment = {
  production: true,
  staging: false,
  baseURL: "https://template.jarabeapi.com/api"
};
```

> Se debe remplazar el **_angular.json_** con el ultimo que esta en la plantilla.

Despues, se puede importar de la siguiente manera: 

```ts
 import { environment } from 'src/environments/environment';
```

Y usar los diferentes modos tal que:

```html
<div class="welcome-screen">
    <h3 *ngIf="environment.production  && !environment.staging">JarabeTemplate</h3>
    <h3 *ngIf="!environment.production && environment.staging">JarabeTemplate staging<h3>
    <h3 *ngIf="!environment.production && !environment.staging">JarabeTemplate LOCAL<h3>
    <img src="/assets/img/logo.png">
</div>
```

Por ultimo se puede hacer este pequeño cambio en el **_api.service.ts_**:

```ts
import { environment } from 'src/environments/environment';

export const BASEURL = environment.baseURL
```

Y al momento de builder para _producción_:

```bash
ionic cordova build android -c production
```

O en el caso de el enviroment _staging_:

```bash
ionic cordova build android -c staging
```

> Si no se especifica ningun argumento de enviroment, se generará una version con el enviroment _default_.