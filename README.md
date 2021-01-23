# React.js

- [Overview](#overview)
- [Architecture](#architecture)
- [Installation](#installation)
- [Modules](#modules)
- [Appendix](#appendix)

## Overview
- React.js is an open-source, front end, JavaScript `library` for building user interfaces or UI components.
- It is maintained by `Facebook` and a community of individual developers and companies.
- React is only concerned with `state management` and `rendering` that state to the `DOM`. 
- React is called `library` instead of `framework` because it only supports `DOM manipulations`. 
  - Other UI framework capabilities like routing, two-way-data-binding will be handled by other libraries.

## Architecture
- Major challenge faced during complex UI codebase is involvement of massive team members.
- More time is spent in determining what code does what. React solves this with below:
    - Complexity of UI code is addressed by break down application into smaller, single-purpose `Components`.
    - Each component maintains a `State`. Based on user interactions, React re-renders components by reacting to change in state.
    - During re-rendering, once the component is ready to render, a virtual snapshot of the change in component state is taken.
    - React now compares the snapshot with the real `DOM` and analyzes the differences. Once it finds the difference, the changes are applied to the UI that’s reflected on the user’s screen. 
    - React uses Virtual DOM (`VDOM`) process to update actual DOM. This has following steps:
      - Create a VDOM with a new state
      - Compare it with older VDOM
      - Update only different nodes in real DOM
      - Assign new VDOM as an older VDOM
    - [Video - How VDOM works](https://www.youtube.com/watch?v=BYbgopx44vo)

![](./01-Images/01-ReactArchitecture.png)

## Installation
- React installation require below:
  - **React**
    - **Core:**
      - `React` is a javascript library, designed for building better user interfaces.
      - It is used to provide `component`, `classes`, `createelement`, etc.
    - **DOM:**
      - `React-DOM` is a complimentary library to React which glues React to the browser DOM.
      - It provides methods like `render()` or `findDOMNode()`
  - **Babel 7.9**
    - It is used for latest ECMAScript and JSX syntax support from React 17.
    - Below package will be used
      - `babel-core:` The main engine of babel plugin.
      - `babel-preset-env:` ECMAScript support.
      - `babel-preset-react:` Compiles JSX syntax to javascript.
      - `babel-loader:` Used to bridge communication between Webpack and Babel.
  - **Webpack 5**
    - It is most widely used and an accepted `module bundler` and `task runner` throughout React.js community.
    - Below package will be used
      - `webpack:` The main engine of webpack plugin.
      - `webpack-cli:` Allow to access webpack commands through CLI.
      - `webpack-dev-server:` A minimal server for client-side development.
      - `html-webpack-plugin:` Generate a html file and hooks with `index.js` file.
      - `html-loader:` Export html as string to be read by webpack.
- HelloWorld React App steps
  ```sh
  # Initialize NPM Project
  npm init -y

  # Required during Runtime
  npm i -S react react-dom

  # Required during Development-only
  npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader
  npm i -D webpack webpack-cli webpack-dev-server html-webpack-plugin
  npm i -D html-loader

  # Babel Configuration
  vi .babelrc
    {
        "presets": [
            "@babel/preset-env", 
            "@babel/preset-react"
        ],
        {
            "runtime": "automatic"
        }
    }

  # Webpack Configuration
  vi webpack.config.js

    const path = require('path');
    const HTMLWebpackPlugin = require('html-webpack-plugin');
    
    module.exports = {
        mode: 'development',
        entry: path.resolve(__dirname, './src/index.js'),
        module: {
            rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: [
                    {
                        loader:'babel-loader'
                    }
                ]
            },
            {
                test: /\.html$/i,
                use: [
                    {
                        loader: 'html-loader'
                    }
                ]
            }
            ],
        },
        devServer: {
          historyApiFallback: true,
          contentBase: path.join(__dirname, 'dist'),
          compress: true,
          port: 9000
        },
        resolve: {
            extensions: ['*', '.js', '.jsx'],
        },
        plugins: [
            new HTMLWebpackPlugin({
                template: './src/index.html',
                filename: './index.html'
            })
        ],
    
        output: {
            path: path.resolve(__dirname, './dist'),
            filename: 'index.js',
        }
    };
    
  # NPM Script Update
  "scripts": {
      # This is not working, webpack server. Any help really appreciated.
      "start": "webpack-dev-server --mode development --open --hot",
      "build": "webpack --mode production"
  }   
  
  # Folders for Source and Webpack Final Code
  mkdir -m777 src
  mkdir -m777 dist

  # Create index.js and index.html
  ```
  <pre>
  <a href=./02-MyDev/01/HelloWorld/src/index.js>index.js</a>
  <a href=./02-MyDev/01/HelloWorld/src/index.html>index.html</a>
  <pre>
  
  ```sh
  # Run in Dev Mode
  npm start

  # Production Mode
  npm run build
  ```

- React team created sample code generator 
  ```sh
  npx create-react-app <app name>
  cd <app name>
  npm install
  npm start
  ```

## Modules
Below are the basic building blocks of React.js
- Components
- JSX
- State
- Props
- Event Handler
- Lifecycle
- Forms
- Hooks
- Router
- Redux
- Material UI
- Storybook
- Jest

## Appendix
- [React](https://reactjs.org/)
- [React Video Tutorial - Codevolution](https://www.youtube.com/watch?v=QFaFIcGhPoM&list=PLC3y8-rFHvwgg3vaYJgHGnModB54rxOk3)
- [React Live Coding Tutorial](https://scrimba.com/learn/learnreact)
- [React Setup Video](https://www.youtube.com/watch?v=ihhPyqfdbjo&t=514s)
- [React 17 Setup](https://iamabhirupdatta.medium.com/setting-up-react-17-with-webpack-and-babel-part-1-e11b674a6102)