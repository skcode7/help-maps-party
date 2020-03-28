# help-maps-party

> Aplicación web para posicionar recursos en un mapa.

Demo: https://help-maps-party.firebaseapp.com/

Útil para aquellas comunidades locales que necesiten saber donde se encuentran las posibilidades más cercanas: personas que necesitan ayuda, personas que ofrecen ayuda, wifis abiertas, comercios cercanos abiertos, etc


Puede emplearse de dos formas:

1. Si eres desarrollador web puedes descargarla y emplearla en tu comunidad.
2. Si tienes una comunidad y crees que puede ayudarte, contacta conmigo (twitter: @delineas)

Para el primer perfil en el repositorio de código puedes encontrar la información de instalación.

Para el segundo, comentar que el despliegue en internet de la aplicación tiene coste cero aprovechando recursos disponibles en la nube. 

La versión de demostración muestra parques de Madrid, pero es solo eso, una versión de demostración. Cada comunidad tendría su propia instalación independiente.

La aplicación no trata de sustituir la potencia de servicios como Google Maps u otras aplicaciones de empresas e instituciones, lo que pretende es estar disponible para grupos pequeños que necesiten una herramienta así para organizarse.

## Características

- Navegación por los recursos a través del mapa y del listado 
- Posicionamiento del usuario en del mapa
- Búsqueda por nombre de lugares y calles usando el servicio de openstreetmaps
- Añadir recursos a través de la interfaz del propio mapa
- Almacenamiento en la nube de Firebase (gratuita hasta un límite de peticiones)
- Puede instalarse como aplicación de escritorio en móvil

## Stack tecnológico

- Vue
- Vue Cli
- Vuex
- Leaflet
- Buefy / Bulma
- Vuefire / Firebase

## Requisitos de instalación

La aplicación se divide en dos partes diferenciadas.

1. El frontal o *frontend* es la que ve el usuario cuando accede a la web.
2. El servidor o *backend* es donde se almacenan los datos que aparecen en el mapa

La parte del frontal está descrita más abajo en *Instalación del proyecto*.

Para la parte del servidor es necesario crear una cuenta gratuita de Firebase. 

Puedes seguir la guía que describen aquí, con algunos matices:
https://firebase.google.com/docs/web/setup?hl=es

### Paso 1: Crea un proyecto de Firebase

Crear la cuenta en Firebase (necesitas una cuenta de Google)

La cuenta gratuita tiene algunas limitaciones que espero no sea necesario que amplies. Revísalo aquí: https://firebase.google.com/pricing

### Paso 2: Registra tu app

Sigue los pasos descritos.

El paso de "Firebase Hosting" es opcional.

### Paso 3: Agrega los SDK de Firebase y, luego, inicializa Firebase

Este paso ya está hecho en el código del proyecto.

Si es muy importante la referencia que aparece bajo el título: "Objeto de configuración de Firebase"

Si no sabes como conseguirlo visita esta página:
http://support.google.com/firebase/answer/7015592?hl=es

Y sigue los pasos bajo el título "Cómo obtener un fragmento de configuración de tu app web"

### Paso 4: Crea una base de datos en Cloud Firestore

En este momento necesitas seguir los pasos descritos en este enlace:
https://firebase.google.com/docs/firestore/quickstart?hl=es

Solo los descritos en el título "Crea una base de datos Cloud Firestore"

Crea una colección con un nombre que luego usarás más adelante.

### Parametrización

Los parámetros que has conseguido de Firebase hay que trasladarlos a la aplicación.

Para eso tienes que crear una copia del fichero .env.example y llamarlo .env.

```
cp .env.example .env
```

A continuación edita ese fichero y coloca los datos necesarios que has copiado desde Firebase.

Por ejemplo si tienes algo así:

```javascript
var firebaseConfig = {
  apiKey: "api-key",
  authDomain: "project-id.firebaseapp.com",
  databaseURL: "https://project-id.firebaseio.com",
  projectId: "project-id",
  storageBucket: "project-id.appspot.com",
  messagingSenderId: "sender-id",
  appID: "app-id",
};
```

El fichero `.env` quedaría así:
```ini
VUE_APP_API_KEY=api-key
VUE_APP_AUTH_DOMAIN=project-id.firebaseapp.com
VUE_APP_DATABASE_URL=https://project-id.firebaseio.com
VUE_APP_PROJECT_ID=project-id
VUE_APP_STORAGE_BUCKET=project-id.appspot.com
VUE_APP_MESSAGING_SENDER_ID=sender-id
VUE_APP_APP_ID=app-id
VUE_APP_MEASUREMENT_ID=
```

Esto es **indispensable** para que funcione correctamente.


### Configuraciones de la aplicación

En el fichero `/src/settings.js` hay algunas configuraciones.

- `center`: Son las coordenadas geográficas donde quieres que se situe el mapa de inicio.
- `collectionName`: Es el nombre de la colección que has creado en Firestore para usarla de almacenamiento.

## Despliegue del frontend en la nube

Las instrucciones para desplegar el sitio en la nube puedes seguirlas en la página de Vue Cli.
https://cli.vuejs.org/guide/deployment.html

### Despliegue en firebase

Es la opción más sencilla de todas, proque ya tenemos la configuración hecha.

Seguiremos los pasos descritos en https://cli.vuejs.org/guide/deployment.html#firebase

1. Instalar `npm install -g firebase-tools``
2. Ejecutar `firebase init``
3. Te pedirá hacer login en la consola de Firebase
4. La consola te preguntará qué quieres hacer, elige "hosting"
5. Selecciona el proyecto en el que quieres hacer el despliegue. Si has completado los pasos anteriores lo tendrás ya creado, así que seleccionalo.
6. La carpeta `public` de tu app es `dist`(por defecto viene definido `public`)
7. Te pregutna si es una aplicación de una sola página, responde `Y`
8. Has terminado la configuración, lanza una *build*  con `npm run build``
9. Lanza el comando `firebase deploy --only hosting``
10. Ya tienes la aplicación desplegada

### Despliegue en now

El despliegue en la plataforma de `zeit now`.

0. Necesitarás crear una cuenta en https://now.sh/
1. Instalar cliente de now con `npm i -g now`
2. En la carpeta raíz del proyecto en local, ejecutar `now` 
3. Seguir los pasos que te va indicando.

Es necesario configurar las variables de entorno de forma concreta desde nuestro entorno local
https://zeit.co/docs/v2/build-step#using-environment-variables-and-secrets

## Instalación del frontend
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
