# React Manual Toolchain Setup

Select the parts you want to use. No Create-React_App used, building each part of the tool chain one step at a time. Read 
the documentation for each tool you go to confirm you are configuring for the current version of each tool

## Initialise Yarn Project 
<i>[git commit 86222aea3fb79cd95df4a2906e9d7f12b5cab7af]

If you prefer npm you can replace each usage of yarn with npm

    yarn init

    # directories
    mkdir src
    mkdir public
    mkdir dist
    # single command
    yarn init && mkdir src && mkdir public && mkdir dist

    # sub directories
    mkdir src/app
    mkdir src/component
    mkdir src/css
    # single command
    mkdir src/app && mkdir src/component && mkdir src/css

    # add some files to include the directories in git
    touch dist/bundle.js && touch public/index.html 
    touch src/app/index.ts && touch src/component/App.tsx && touch styles.css
    
Note you should edit the included .gitignore to suit your needs.


## Typescript support [Optional]
<i>[git commit 0538ff9c6208cf0d04da28b3808f426ff336f7ae]

This is the basic setup to enable typescript support in your project. You really need to integrate ts support
into babel and webpack for a complete working tool chain.

    yarn add -D typescript ts-loader

### setup proj dir for webpack

    touch tsconfig.json


tsconfig.json simple configuration to support JSX and compile TypeScript down to ES5

    {
        "compilerOptions": {
        "outDir": "./dist/",
        "noImplicitAny": true,
        "module": "es6",
        "target": "es5",
        "jsx": "react",
        "allowJs": true,
        "moduleResolution": "Node",
        "allowSyntheticDefaultImports": true
        }
    }

See TypeScript’s documentation to learn more about [tsconfig.json configuration options](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)

## Webpack

Webpack is a bundler so it takes your source code, runs any transformations configured through any plugins and tools such as 
Babel. Created a index_bundle.js filed containing your application logic and writes this to /dist/index_bundle.js

    yarn add -D webpack webpack-cli html-webpack-plugin webpack-dev-server
    touch webpack.config.js

webpack.config.js
    
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const path = require('path');


    module.exports = {
        entry: './src/app/index.ts',
        mode: 'development',
        module: {
            rules: [
                {
                test: /\.tsx?$/,
                use: 'ts-loader',
                exclude: /node_modules/,
                },
            ],
        },
        resolve: {
            extensions: ['.tsx', '.ts', '.js'],
        },
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'index_bundle.js',
        },

        plugins: [new HtmlWebpackPlugin({
            filename: 'public/index.html'
        })]
    };

This will direct webpack to enter through ./src/app/index.ts, load all .ts and .tsx files through the ts-loader, and output a
index_bundle.js file in the ./dist directory.

Adding lodash and types.

    yarn add lodash
    yarn add -D @types/lodash

Now lets the import of lodash in our ./src/app/index.ts. 

    import * as _ from ‘lodash’;

To make imports do this by default and keep import _ from ‘lodash’; syntax in TypeScript, set “allowSyntheticDefaultImports” : true 
and “esModuleInterop” : true in your tsconfig.json file. This is related to TypeScript configuration and mentioned in our 
guide only for your information.

### Test webpack is working

    yarn webpack

### add webpack serve to package.json

    # package.json
    +   “scripts”: {
         “start”: “webpack serve”
        },

You can now run your app with a dev server with the following command
    
    yarn start