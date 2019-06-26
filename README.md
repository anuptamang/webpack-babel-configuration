## Webpack / Babel configuration

# Go to `https://github.com/anuptamang/webpack-babel-starter` for Webpack / Babel Starter files

# Got to your working folder in command line and follow these instructions step-by-step

# First lets create the default entry point folder and files, folder `src` and inside this folder `index.js` and add some js code in that file

1. run `npm init`
2. run `npm i --save-dev webpack webpack-cli`
3. now change scripts option in package.json
   "scripts": {
   "start": "webpack --mode development",
   "build": "webpack --mode production"
   }

4. now we can run `npm run start`, you should notice there is now `dist` folder auto-generated and there is inside `main.js`

5. now create `webpack.config.js` file and config custom entry, output etc.

# `webpack.config.js` file should be like this at this stage

    const path = require('path');

    module.exports = {
        entry: path.resolve(__dirname, 'src'),
        output: {
            path: path.resolve(__dirname, 'build'),
            filename: 'bundle.js'
        }
    };

# now lets run `npm run build`, there should be folder named `build` generated and inside that folder there is `bundle.js` from this state we done need `dist` folder, so lets delete that

6. now lets run `npm i --save-dev webpack-dev-server`
7. now add in `webpack.config.js` devServer info
   devServer: {
   port: 3000,
   contentBase: path.resolve(\_\_dirname, 'build')
   }

# `webpack.config.js` file should be like this at this stage

    const path = require('path');

    module.exports = {
        entry: path.resolve(__dirname, 'src'),
        output: {
            path: path.resolve(__dirname, 'build'),
            filename: 'bundle.js'
        },
        devServer: {
            port: 3000,
            contentBase: path.resolve(__dirname, 'build')
        }
    };

# change in `package.json`

"scripts": {
"start": "webpack-dev-server --mode development",
"build": "webpack --mode production"
}

# also we need to create `index.html` file in the folder `build`, and connect `bundle.js` file for webpack dev serve

# now our main working folder is `app` and build folder is `build`

..........This is the end of webpack bundling process..............

# Now we can see it in action

1. Now run `npm run start` ==> you should be seeing in command line `Project is running at http://localhost:3000/` and other info too.
2. FInally to build file `npm run build`

# Now to add Babel to your project

1. `npm i --save-dev babel-core babel-loader@7 babel-preset-env`, there may be version issues so read the errors and install again required version
2. config `module` in babel in `webpack.config.js` add below option:

   module: {
   rules: [
   {
   test: /\.js\$/,
   exclude: /node_modules/,
   use: ['babel-loader']
   }
   ]
   }

# `webpack.config.js` file should be like this at this stage

    const path = require('path');

    module.exports = {
        entry: path.resolve(__dirname, 'src'),
        output: {
            path: path.resolve(__dirname, 'build'),
            filename: 'bundle.js'
        },
        devServer: {
            port: 3000,
            contentBase: path.resolve(__dirname, 'build')
        },

        module: {
            rules: [
                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    use: ['babel-loader']
                }
            ]
        }
    };

3. create `.babelrc` file and assign object propery, "presets": ["env"]

# file should be like this

    {
    "presets": ["env"]
    }

4. Now run `npm run start`
5. to build file `npm run build`
