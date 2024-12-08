# Steps to Create a React Native Web App

## 1. Set Up the Project
1. Create a new project folder and initialize it:
   ```bash
   mkdir my-react-native-web-app
   cd my-react-native-web-app
   npm init -y
   ```

## 2. Install Dependencies
Install the necessary packages:
```bash
npm install react@18 react-dom@18 react-native@0.76 react-native-web@0.18 --legacy-peer-deps
```

Install development dependencies for Webpack and Babel:
```bash
npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env @babel/preset-react html-webpack-plugin
```

## 3. Configure Webpack
Create a `webpack.config.js` file in the root directory:
```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  resolve: {
    alias: {
      'react-native$': 'react-native-web',
    },
    extensions: ['.web.js', '.js'],
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
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
  ],
  devServer: {
    static: path.join(__dirname, 'dist'),
    compress: true,
    port: 3000,
  },
};
```

## 4. Configure Babel
Create a `.babelrc` file in the root directory:
```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## 5. Set Up the Project Structure
Create the following directory and file structure:
```
my-react-native-web-app/
├── public/
│   └── index.html
├── src/
│   ├── App.js
│   └── index.js
├── webpack.config.js
├── .babelrc
├── package.json
```

## 6. Add the HTML Template
Create `public/index.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React Native Web App</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

## 7. Add the Main React Native Component
Create `src/App.js`:
```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello, React Native Web!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 24,
    color: 'blue',
  },
});
```

## 8. Add the Entry Point
Create `src/index.js`:
```javascript
import { AppRegistry } from 'react-native';
import App from './App';
import appConfig from '../app.json';

AppRegistry.registerComponent(appConfig.name, () => App);
AppRegistry.runApplication(appConfig.name, {
  initialProps: {},
  rootTag: document.getElementById('root'),
});
```

## 9. Add a Dummy `app.json`
Create `app.json` in the root directory:
```json
{
  "name": "MyReactNativeWebApp"
}
```

## 10. Update `package.json` Scripts
Add these scripts to the `scripts` section in `package.json`:
```json
"scripts": {
  "start": "webpack serve --mode development",
  "build": "webpack --mode production"
}
```

## 11. Start the Development Server
Run the following command to start the app in development mode:
```bash
npm start
```

Open your browser at `http://localhost:3000` to view the app.

## 12. Build for Production
When ready to deploy, create a production build:
```bash
npm run build
```

The optimized files will be in the `dist/` directory.

