# Setup-React-application-manually
Setting up a React application manually using Webpack and Babel involves several steps. I'll guide you through the process.

**Steps:**

## Step 1: Set Up Project Structure
**Create a new directory for your project and navigate into it:**
```bash
    mkdir my-react-app
    cd my-react-app
```

## Step 2: Initialize npm
Initialize a new npm project:
```bash
npm init -y
```
This will create a package.json file in your project directory.

### Step 3: Install Dependencies
You'll need to install several dependencies, including React, ReactDOM, Webpack, Babel, and related plugins.

### Install React and ReactDOM:
```bash
npm install react react-dom
```
### Install Webpack and Webpack CLI:
```bash
npm install webpack webpack-cli html-webpack-plugin webpack-dev-server --save-dev
```

### Install Babel and related plugins:
```bash
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader --save-dev
```

## Step 4: Configure Babel
Create a .babelrc file in the root of your project and add the following configuration:
```bash
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```
## Step 5: Configure Webpack
Create a webpack.config.js file in the root of your project and add the following configuration:
```bash
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
  ],
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    compress: true,
    port: 9000,
  },
};
```

## Step 6: Create Source Files
Create the necessary directories and files:
```bash
mkdir src public
touch src/index.js src/App.js public/index.html
```
public/index.html:
```bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React App</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```
src/index.js:
```bash
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App/>)
```
src/App.js:
```bash
import React from 'react';

const App = () => {
  return (
    <div>
      <h1>Hello, React!</h1>
    </div>
  );
};

export default App;
```

## Step 7: Add Scripts to package.json
Update the scripts section in your package.json file to include Webpack commands:
```bash
"scripts": {
  "start": "webpack serve --mode development",
  "build": "webpack --mode production"
}
```
## Step 8: Start the Development Server
Run the development server:
```bash
npm start
```
