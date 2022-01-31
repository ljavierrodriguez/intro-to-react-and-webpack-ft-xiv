# CREAR UN PROYECTO DE REACT CON WEBPACK

### 1.- Iniciar Proyecto con npm

    $ npm init -y


### 2.- Creamos el archivo index.js en la ruta src/index.js

    ... crear la carpeta src con el archivo index.js dentro de la misma.

### 3.- Instalamos webpack

    $ npm i --save-dev webpack webpack-dev-server webpack-cli


### 4.- Configurar webpack en nuestro archivo package.json

    {
        ...
        "scripts": {
            "start": "webpack serve --mode development",
            "test": "echo \"Error: no test specified\" && exit 1"
        },
        "keyworks": [],
        ...
    }

### 5.- Crear y configurar el archivo webpack.config.js

    module.exports = {
        entry: "./src/index.js",
        output: {
            path: '/build',
            filename: 'bundle.js'
        },
        devServer: {
            contentBase: './build'
        }
    }

### 6.- Modificar el archivo package.json y modificiar el script (start) y quede de la siguiente forma

    {   
        ...
        "scripts": {
            "start": "webpack serve --config ./webpack.config.js --mode development",
            "test": "echo \"Error: no test specified\" && exit 1"
        },
        "keyworks": [],
        ...
    }

### 7.- Creadmos nuestro archivo index.html dentro de la carpeta public

    #public/index.html

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <div id="app"></div>
    </body>
    </html>

### 8.- Instalamos las librerias necesarias de babel

    $ npm i --save-dev @babel/core @babel/preset-env babel-loader

### 9.- Configurar en el package.json babel

    {
        ...
        "babel": {
            "presets": [
            "@babel/preset-env"
            ]
        }
        ...
    }

### 10.- Configurar loader de babel en nuestro archivo webpack.config.js

    {
        ...
        module: {
            rules: [
                {
                    test: /\.(js|jsx)$/,
                    exclude: /node_modules/,
                    use: ['babel-loader']
                }
            ]
        },
        resolve: {
            extensions: ['*', '.js', '.jsx']
        },
        ...
    }

### 11.- crear el archivo .babelrc

    {
        "presets": [
        "@babel/preset-env"
        ]
    }

### 12.- Instalar react con babel 

    $ npm i --save-dev @babel/preset-react
    $ npm i --save react react-dom

### 13.- Configurar .babelrc aceptando react

    {
        "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
        ]
    }

### 14.- Modificar el contenido de nuestro index.js por el siquiente contenido

    import React from 'react';
    import ReactDOM from 'react-dom';

    const content = <h1>Hola desde React</h1>;

    ReactDOM.render(content, document.querySelector('#app'))

#### 15.- Instalar HtmlWebpackPlugin

    $ npm install --save-dev html-webpack-plugin


### 16.- Configurar HtmlWebpackPlugin

    module.exports = {
        ...
        plugins: [new HtmlWebpackPlugin({
            template: path.resolve(__dirname, './public/index.html'),
            filename: 'index.html'
        })],
        ...
    }
