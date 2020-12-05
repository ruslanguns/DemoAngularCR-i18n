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

Sin más, este tutorial es bastante sencillo, te invito a que vallas a la documentación oficial de Angular: https://angular.io/guide/i18n

## Autor
- Ruslán González
- Twitter: [@ruslangonzalez](https://twitter.com/ruslangonzalez)
- Web: [rusgunx.tk](https://rusgunx.tk)

