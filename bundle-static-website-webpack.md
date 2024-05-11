# Bundle a Static Website using Webpack

To bundle a static website using Webpack, you'll need to create a `webpack.config.js` file to configure Webpack. Here's a basic example to get you started:

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
  entry: "./src/index.js", // Entry point of your application
  output: {
    filename: "bundle.js", // Output bundle file name
    path: path.resolve(__dirname, "dist"), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader", // Use Babel to transpile JavaScript files
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"], // Use style-loader and css-loader for CSS files
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: ["file-loader"], // Use file-loader for image files
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(), // Clean the 'dist' directory before each build
    new HtmlWebpackPlugin({
      template: "./src/index.html", // Generate HTML file using template
    }),
  ],
};
```

In this configuration:

- `entry` specifies the entry point of your application.
- `output` specifies the bundle file name and output directory.
- `module.rules` define loaders to handle different types of files. Here, we're using Babel for JavaScript files, style-loader and css-loader for CSS files, and file-loader for image files.
- `plugins` include CleanWebpackPlugin to clean the 'dist' directory before each build, and HtmlWebpackPlugin to generate an HTML file using a template (usually `index.html` in the 'src' directory).

Make sure to install the necessary dependencies (`babel-loader`, `style-loader`, `css-loader`, `file-loader`, `html-webpack-plugin`, `clean-webpack-plugin`) via npm or yarn before running Webpack.

Once you have this `webpack.config.js` file set up, you can run Webpack to bundle your static website by executing the `webpack` command in your terminal. The bundled files will be generated in the 'dist' directory.

## Multi-module config for bundling each page separately

To create a multi-module configuration for bundling each page separately in a static website using Webpack, you can modify the `webpack.config.js` file to handle multiple entry points. Here's how you can achieve this:

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
  entry: {
    index: "./src/pages/index/index.js", // Entry point for the index page
    about: "./src/pages/about/about.js", // Entry point for the about page
    contact: "./src/pages/contact/contact.js", // Entry point for the contact page
  },
  output: {
    filename: "[name].bundle.js", // Output bundle file name with dynamic name based on entry point
    path: path.resolve(__dirname, "dist"), // Output directory
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader", // Use Babel to transpile JavaScript files
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"], // Use style-loader and css-loader for CSS files
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: ["file-loader"], // Use file-loader for image files
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(), // Clean the 'dist' directory before each build
    new HtmlWebpackPlugin({
      template: "./src/pages/index/index.html", // Generate HTML file using template for the index page
      filename: "index.html", // Output file name for the index page
      chunks: ["index"], // Include only 'index' bundle in this HTML file
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/about/about.html", // Generate HTML file using template for the about page
      filename: "about.html", // Output file name for the about page
      chunks: ["about"], // Include only 'about' bundle in this HTML file
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/contact/contact.html", // Generate HTML file using template for the contact page
      filename: "contact.html", // Output file name for the contact page
      chunks: ["contact"], // Include only 'contact' bundle in this HTML file
    }),
  ],
};
```

In this configuration:

- `entry` specifies multiple entry points for each page of the website.
- `output.filename` uses a dynamic placeholder `[name]` to generate bundle file names based on the entry point name.
- Multiple `HtmlWebpackPlugin` instances are used to generate HTML files for each page of the website. Each plugin is configured with a specific template and output file name, and includes only the corresponding bundle in the HTML file using the `chunks` option.

With this configuration, when you run Webpack, it will generate separate bundles and HTML files for each page of the website in the 'dist' directory.

## Dev server config for HMR for local development

To add webpack dev server configuration for hot module replacement (HMR) for local development, you can update the `webpack.config.js` file to include the devServer option. Here's how you can modify the configuration:

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
  entry: {
    index: "./src/pages/index/index.js",
    about: "./src/pages/about/about.js",
    contact: "./src/pages/contact/contact.js",
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: ["file-loader"],
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: "./src/pages/index/index.html",
      filename: "index.html",
      chunks: ["index"],
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/about/about.html",
      filename: "about.html",
      chunks: ["about"],
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/contact/contact.html",
      filename: "contact.html",
      chunks: ["contact"],
    }),
  ],
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 3000,
    hot: true, // Enable hot module replacement
  },
};
```

In this configuration:

- `devServer` option is added to configure the webpack dev server.
- `contentBase` specifies the directory from which static files should be served.
- `compress` enables gzip compression for all assets served by the dev server.
- `port` specifies the port number on which the dev server will run.
- `hot: true` enables hot module replacement, allowing modules to be replaced without a full page reload.

With this configuration, you can run `webpack serve` or `npx webpack serve` to start the webpack dev server with hot module replacement enabled for local development.

## Use EJS template engine

To use the EJS (Embedded JavaScript) template engine with Webpack HtmlWebpackPlugin, you need to install the `ejs-loader` package and update the webpack configuration to support EJS templates. Here's how you can do it:

First, install the `ejs-loader` package:

```bash
npm install ejs-loader --save-dev
```

Then, update the webpack configuration to use EJS templates:

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
  entry: {
    index: "./src/pages/index/index.js",
    about: "./src/pages/about/about.js",
    contact: "./src/pages/contact/contact.js",
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: ["file-loader"],
      },
      {
        test: /\.ejs$/, // Add a rule to handle EJS files
        loader: "ejs-loader",
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: "./src/pages/index/index.ejs", // Path to EJS template for the index page
      filename: "index.html", // Output file name for the index page
      chunks: ["index"],
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/about/about.ejs", // Path to EJS template for the about page
      filename: "about.html", // Output file name for the about page
      chunks: ["about"],
    }),
    new HtmlWebpackPlugin({
      template: "./src/pages/contact/contact.ejs", // Path to EJS template for the contact page
      filename: "contact.html", // Output file name for the contact page
      chunks: ["contact"],
    }),
  ],
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 3000,
    hot: true,
  },
};
```

In this configuration:

- We've added a new rule to handle `.ejs` files using the `ejs-loader`.
- Each `HtmlWebpackPlugin` instance now points to an EJS template file (e.g., `'./src/pages/index/index.ejs'`, `'./src/pages/about/about.ejs'`, `'./src/pages/contact/contact.ejs'`).

Ensure that you have EJS template files created at the specified paths and that they contain valid EJS syntax for dynamic content generation.

### About chunks config in the above

In the webpack configuration provided, the `chunks` configuration option in the HtmlWebpackPlugin plugin determines which JavaScript bundles are included in the generated HTML file.

When you have multiple entry points (e.g., for different pages of your website), webpack generates separate JavaScript bundles for each entry point. By specifying the `chunks` option in HtmlWebpackPlugin, you can control which of these bundles are injected into the HTML file associated with that HtmlWebpackPlugin instance.

For example:

```javascript
new HtmlWebpackPlugin({
  template: './src/pages/index/index.html',
  filename: 'index.html',
  chunks: ['index']
}),
```

In this example:

- `chunks: ['index']` specifies that only the JavaScript bundle associated with the 'index' entry point will be included in the generated 'index.html' file.
- If you have multiple entry points (e.g., 'about', 'contact'), you would specify the relevant chunk names for each HtmlWebpackPlugin instance accordingly.

This allows you to create separate HTML files for each page of your website, and include only the necessary JavaScript bundles for each page to keep the bundle size smaller and improve performance.
