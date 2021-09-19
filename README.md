# React Manual Toolchain Setup

Select the parts you want to use. No Create-React_App used, building each part of the tool chain one step at a time.

## Initialise Yarn Project 
[git commit 86222aea3fb79cd95df4a2906e9d7f12b5cab7af]

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


