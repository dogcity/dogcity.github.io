---
layout: post
title: Implementando Babel JavaScript en el BackEnd
description: "Simple implementación de Babel en el Back"
tags: [babel backend]
author: José Ortega
---

# BABEL
Es un compilador de codigo JavaScript que mediante plugins/presets nos ayuda a disponibilizar nuestro codigo al estandar (ES5) para navegadores, de esta forma podemos escribir con las nuevas versiones o herramientas sin preocuparnos por si funcionará en un navegador
La configuración que se mostrará está pensada en la utilización de babel en el BackEnd, ya que en el Front ya está solucionado por create-react-app de React

## Instalar dependencias
Primero debemos instalar las dependencias y presets
```
yarn add -D @babel/cli @babel/node @babel/core @babel/preset-env
```

## Crear archivo de configuración
Ahora debemos realizar la configuración de babel mediante el archivo .babelrc que debemos crear

1. Crear archivo
```shell=
nano .babelrc
```
2. Agregar configuración: con esta configuración disponibilizamos babel para cualquier version de JavaScript
```shell=
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "node": true
        }
      }
    ]
  ]
}
```

## Agregar scripts al package.json
1. Start: para ejecutar el proyecto en ambiente de desarrollo, con la transpilación de babel en tiempo de ejecución
```shell=
"start": "nodemon --exec babel-node src/index"
```
2. Build: para transpilar el proyecto y generar una salida estandar para producción
```shell=
"build": "babel src/ --out-dir build"
```
3. Serve: para inicializar el proyecto en el ambiente de producción, con los datos transpilados por babel con el script "build"
```shell=
"serve": "node build/index"
```

Listo, ya tenemos Babel integrado y listo para usar en desarrollo o producción

