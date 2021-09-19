# React Manual Toolchain Setup

Select the parts you want to use. No Create-React_App used, building each part of the tool chain one step at a time.

#   Initialise Yarn Project []

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


