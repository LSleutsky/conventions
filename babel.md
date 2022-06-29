```js
// babel.config.js

const path = require(`path`);

const getAliases = () => ({
  root: __dirname,
  app: path.join(__dirname, `app`),
  assets: path.join(__dirname, `app/assets`),
  components: path.join(__dirname, `app/components`),
  config: path.join(__dirname, `app/config`),
  containers: path.join(__dirname, `app/containers`),
  utils: path.join(__dirname, `app/utils`)
});

module.exports = api => {
  api.cache(true);

  return {
    comments: true,
    env: {
      production: {
        plugins: [
          `@babel/plugin-transform-react-constant-elements`,
          [`babel-plugin-transform-react-class-to-function`, { memo: true }],
          [
            `transform-react-remove-prop-types`,
            {
              mode: `remove`,
              removeImport: true
            }
          ]
        ]
      }
    },
    presets: [
      [
        `@babel/preset-react`,
        {
          runtime: `automatic`,
          development: !!process.env.IS_LOCAL,
          importSource: `@welldone-software/why-did-you-render`
        }
      ],
      `@babel/preset-env`
    ],
    plugins: [
      `lodash`,
      `transform-react-router-optimize`,
      `@babel/plugin-syntax-dynamic-import`,
      `@babel/plugin-proposal-export-default-from`,
      `@babel/plugin-proposal-class-properties`,
      `@babel/plugin-proposal-optional-chaining`,
      `@babel/plugin-proposal-nullish-coalescing-operator`,
      `@emotion`,
      [
        `babel-plugin-styled-components`,
        { minify: true, pure: true, ssr: true, transpileTemplateLiterals: true }
      ],
      [`babel-plugin-module-resolver`, { alias: getAliases() }],
      [
        `transform-imports`,
        {
          'react-bootstrap': {
            transform: importName => `react-bootstrap/lib/${importName}`,
            preventFullImport: true
          },
          lodash: {
            transform: importName => `lodash/${importName}`,
            preventFullImport: true
          },
          '@material-ui/core': {
            transform: importName => `@material-ui/core/${importName}`,
            preventFullImport: true
          }
        }
      ]
    ]
  };
};
```
