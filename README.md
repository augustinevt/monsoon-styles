# By convention, we put say

@import '@monsoon_inc/monsoon-styleguide/lib/<file-to-import>'

in a index.scss that we then import into the App.js file.

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
