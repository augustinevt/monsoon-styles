# develop

in monsoon-styles : `npm link`
in root of app : 'npm link @monsoon_inc/monsoon-styles2'


# By convention, we import like this:

`@import '@monsoon_inc/monsoon-styleguide/lib/<file-to-import>`

in a index.scss that we then import into the App.js file (although you can import it into a JS file, just take the "@" off of the previous line)

Also, in order to do that, you need to be tell webpack to look for sass in node_modules

```
  exports.loadStyles = ({include, exclude} = {}) => ({
    module: {
      rules: [
        {
          test: /\.(css|scss)$/,
          include,
          exclude,
          use: [
            { loader: 'style-loader', options: {sourceMap: true}},
            { loader: 'css-loader', options: {sourceMap: true, modules: false}},
            {
              loader: 'postcss-loader',
              options: {
                plugins: () => ([
                  require('autoprefixer')()
                ]),
              },
            },
            { loader: 'resolve-url-loader'},
            { loader: 'sass-loader', options: {
              sourceMap: true,
              includePaths: ['node_modules', 'src', '.']
            }}
          ]
        }
      ]
    }
  });
```
