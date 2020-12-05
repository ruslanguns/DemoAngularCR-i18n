# I18nDemo

En este proyecto tengo el pequeño ejemplo que llevé a cabo en la charla que he dado en la comunidad de AngularCR.

El enlace al video lo puedes ver aquí: https://youtu.be/hZA_gmbS65A

También puedes ver los slides aquí: https://docs.google.com/presentation/d/1vJ3zFTsmkd6SkuWQfjaaeziVN1loX4UXiUHYAEodH5w/edit?usp=sharing

## ¿Cómo funciona el proyecto?

Primero tienes que clonar el repositorio y a continuación instalar las dependencias con yarn o npm.

A continuación notarás que he incluido el dist al deploy para que puedan ver los archivos resultantes del comando de generación de traducciones:

```bash
$ ng build --prod --localize
```

Puedes abrir el entorno de desarrollo como comúnmente lo haces usando `ng serve` pero también puedes añadir el determinado lenguaje. Los disponibles en este proyecto son: es, es-CR y en. Entre el es y es-CR no existen diferencias, me faltó ser más creativo, pero si puedes ver la diferencia entre en y es por supuesto.

Para lanzar entonces el entorno de desarrollo de español por ejemplo puedes correr el siguiente comando:

```bash
$ ng serve --configuration=es
```

Por defecto la aplicación se abrirá en el puerto 4200.

Te reto a que la ejecutes en diferentes puertos usando distintos lenguajes:

```bash
$ ng serve --configuration=es-CR --port 4200     # En una terminal
$ ng serve --configuration=es --port 4201     # En otra ventana del terminal
$ ng serve --configuration=en --port 4202     # Y en otra más
```

En este caso lanzarías el entorno de desarrollo en tres distintas ventanas y verías las diferencias y el resultado de tus traducciones.

Sin más, este tutorial es bastante sencillo, te invito a que vallas a la documentación oficial de Angular: https://angular.io/guide/i18n para que produndicez temas más avanzados!

## ¿Cómo se consiguió que esto funcionara?

He seguido los siguientes pasos para conseguir que esto funcionará:

1. He instalado el paquete de @angular/localize

```bash
$ ng add @angular/localize
```

2. A continuación he implementado los atributos al template para decirle las traducciones que llevaré a cabo:

```html
<!-- src/app/app.component.ts -->

<!-- ANTES -->
<h1>Hello AngularCR<h1>

<!-- DESPUÉS -->
<h1 i18n>Hello AngularCR<h1>
```
> Con este cambio he conseguido decirle al compilador y ejecutor de Angular que sepa que hay una frase que deseo añadir al archivo de traducciones.

3. He extraido las traducciones:

```bash
$ ng extract-i18n --output-path src/locale
```
> Esto lee los atributos de los HTML de toda mi aplicación y extrae en un xlf un archivo que por defecto tiene por nombre `messages.xlf` con las configuraciones que le he enviado.

4. He configurado el archivo `angular.json`

```json
// angular.json

"i18n-demo": {
      ...
      "i18n": {
        "sourceLocale": "es-CR",
        "locales": {
          "en": "src/locale/messages.en.xlf",
          "es": "src/locale/messages.es.xlf"
        }
      ...
```
> Aquí le estoy indicando desde dónde leerá los archivos locales, así mismo, le indicamos el lenguaje por defecto en este caso `es-CR`. Recordemos que antes he extraído las frases un archivo llamado messages, pues más adelante debemos crear los archivos `messages.en.xlf` y `messages.es.xlf` con las traducciones adecuadas a cada archivo según el lenguaje que necesitemos. Nota importante, asi es cómo nosotros añadimos más lenguajes a nuestra aplicación.

```
// angular.json

"architect": {
        "build": {
          ...
          "options": {
            ...
            "localize": true,
            "aot": true,
            ...
          },
          "configurations": {
            "es": {
              "localize": ["es"]
            },
            "en": {
              "localize": ["en"]
            },
            "es-CR": {
              "localize": ["es-CR"]
            },
```
> Habilitamos el localize en el Angular CLI en el build y le indicamos que utilice las localizaciones configuradas.

```
// angular.json
"serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "options": {
            "browserTarget": "i18n-demo:build"
          },
          "configurations": {
            "en": {
              "browserTarget": "i18n-demo:build:en"
            },
            "es": {
              "browserTarget": "i18n-demo:build:es"
            },
            "es-CR": {
              "browserTarget": "i18n-demo:build:es-CR"
            },
            "production": {
              "browserTarget": "i18n-demo:build:production"
            }
          }
        },
```
> Hacemos lo mismo para el comando del serve.

5. Creamos a partir del archivo `src/locale/messages.xlf` los respectivos archivos por cada traducción.

```bash
$ mv src/locale/messages.xlf src/locale/messages.es.xlf
$ mv src/locale/messages.xlf src/locale/messages.es.xlf
```

6. Traducimos los archivos.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<xliff version="1.2" xmlns="urn:oasis:names:tc:xliff:document:1.2">
  <file source-language="es-CR" datatype="plaintext" original="ng2.template">
    <body>
      <trans-unit id="6cda0b5bbc17af2d88c28d3057dbc490f782fec0" datatype="html">
        <source>Hello AngularCR</source> <!-- LINEA QUE TRADUCIREMOS EN ESTE EJEMPLO -->
        <context-group purpose="location">
          <context context-type="sourcefile">src/app/app.component.html</context>
          <context context-type="linenumber">1</context>
        </context-group>
      </trans-unit>
    </body>
  </file>
</xliff>
```

> Debemos ver la linea `<source>...</source>` es el texto que hemos crear abajo de ella una propiedad con las etiquetas `<target>...</target>` y colocar dentro de ella la traducción. Hacer lo mismo para cada archivo.

6. Finalmente producimos ya sea nuestro proyecto para deploy final o uno de desarrollo:

```bash
$ ng build --prod --localize     # para producción con el bundle final 

$ ng serve --configuration=es    # para desarrollo con la configuración por cada lenguaje, si no lo especificamos, cogerá el que está por defecto.
```

Y esto es todo. 

Espero que este tutorial les sirva de algo, y por favor, cualquier duda no duden en contactarme.


## Autor
- Ruslán González
- Twitter: [@ruslangonzalez](https://twitter.com/ruslangonzalez)
- Web: [rusgunx.tk](https://rusgunx.tk)

