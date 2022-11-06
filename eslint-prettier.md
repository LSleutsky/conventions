# ESLint

The below is a configuration template for an `.eslintrc.json` file for a typical React project:

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:import/recommended",
    "plugin:prettier/recommended"
  ],
  "parser": "babel-eslint",
  "plugins": ["better-styled-components", "prettier", "react", "simple-import-sort"],
  "env": {
    "browser": true,
    "es6": true,
    "mocha": true,
    "node": true
  },
  "rules": {
    "array-callback-return": "off",
    "better-styled-components/sort-declarations-alphabetically": 2,
    "camelcase": "off",
    "consistent-return": "off",
    "eqeqeq": "off",
    "global-require": "off",
    "jsx-a11y/label-has-associated-control": "off",
    "jsx-a11y/label-has-for": "off",
    "implicit-arrow-linebreak": "off",
    "import/export": "error",
    "import/namespace": "off",
    "import/newline-after-import": ["error", { "count": 1 }],
    "import/no-duplicates": "error",
    "import/no-extraneous-dependencies": "off",
    "import/no-named-as-default": "off",
    "import/no-cycle": "off",
    "import/order": "off",
    "no-confusing-arrow": "off",
    "no-console": ["error", { "allow": ["error", "info", "warn"] }],
    "no-dupe-keys": "error",
    "no-duplicate-case": "error",
    "no-empty": "error",
    "no-mixed-operators": "off",
    "no-nested-ternary": "off",
    "no-var": "error",
    "no-plusplus": "off",
    "no-restricted-imports": ["error", { "patterns": ["../*"] }],
    "no-restricted-syntax": "off",
    "no-underscore-dangle": 0,
    "no-unexpected-multiline": "error",
    "no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
    "one-var": "off",
    "one-var-declaration-per-line": "off",
    "padding-line-between-statements": [
      "error",
      {
        "blankLine": "always",
        "prev": "*",
        "next": [
          "break",
          "class",
          "const",
          "cjs-export",
          "debugger",
          "do",
          "export",
          "for",
          "function",
          "if",
          "let",
          "multiline-const",
          "multiline-let",
          "return",
          "switch",
          "throw",
          "try",
          "while"
        ]
      },
      {
        "blankLine": "always",
        "prev": [
          "class",
          "const",
          "debugger",
          "do",
          "default",
          "export",
          "for",
          "function",
          "if",
          "let",
          "multiline-const",
          "multiline-let",
          "return",
          "switch",
          "try",
          "while"
        ],
        "next": "*"
      },
      {
        "blankLine": "never",
        "prev": ["singleline-const", "singleline-let"],
        "next": ["singleline-const", "singleline-let"]
      },
      {
        "blankLine": "always",
        "prev": ["directive", "cjs-import"],
        "next": "*"
      },
      {
        "blankLine": "always",
        "prev": "*",
        "next": ["directive", "cjs-import"]
      },
      {
        "blankLine": "never",
        "prev": ["cjs-import"],
        "next": ["cjs-import"]
      },
      {
        "blankLine": "never",
        "prev": ["directive"],
        "next": ["directive"]
      }
    ],
    "prefer-const": "error",
    "prettier/prettier": ["error", { "arrowParens": "avoid" }],
    "quotes": [
      2,
      "backtick",
      {
        "allowTemplateLiterals": true,
        "avoidEscape": true
      }
    ],
    "react/destructuring-assignment": "off",
    "react/display-name": "off",
    "react/jsx-filename-extension": "off",
    "react/jsx-indent": "off",
    "react/jsx-no-undef": "error",
    "react/jsx-one-expression-per-line": "off",
    "react/jsx-sort-props": ["error", {
      "ignoreCase": true,
      "reservedFirst": true
    }],
    "react/no-children-prop": "off",
    "react/no-deprecated": 0,
    "react/no-did-update-set-state": "off",
    "react/no-unused-state": "error",
    "react/no-will-update-set-state": "off",
    "react/prop-types": 0,
    "react/sort-comp": 0,
    "react/sort-prop-types": ["error", {
      "ignoreCase": true,
      "sortShapeProp": true
    }],
    "simple-import-sort/exports": "error",
    "simple-import-sort/imports": "error",
    "spaced-comment": ["error", "always", {
      "line": {
        "markers": ["/"],
        "exceptions": ["-", "+"]
      },
      "block": {
        "markers": ["!"],
        "exceptions": ["*"],
        "balanced": true
      }
    }]
  },
  "overrides": [
    {
      "files": ["*.js"],
      "rules": {
        "simple-import-sort/imports": [
          "error",
          {
            "groups": [
              ["^react$", "react-redux", "^react-router", "redux", "^redux-"],
              ["^@", "^\\w"],
              ["^(actions)"],
              ["^(actions)(/.*)(types)"],
              ["^(reducers)(/.*|$)"],
              ["^(selectors)(/.*|$)"],
              ["^(components)(/.*|$)"],
              ["^(containers)(/.*|$)"],
              ["^(hooks)(/.*|$)"],
              ["^(constants)(/.*|$)"],
              ["^(utils)(/.*|$)"],
              ["^(config)(/.*|$)"],
              ["^\\.\\.(?!/?$)", "^\\.\\./?$"],
              ["^\\./(?=.*/)(?!/?$)", "^\\.(?!/?$)", "^\\./?$"],
              ["^.+\\.?(s?css)$"],
              ["^\\u0000"]
            ]
          }
        ]
      }
    },
    {
      "files": ["**/*/types.js"],
      "rules": {
        "padding-line-between-statements": "off"
      }
    }
  ],
  "settings": {
    "import/resolver": "webpack",
    "react": {
      "version": "detect"
    }
  }
}
```

# Prettier

The below is a configuration template for a `.prettierrc.js` file:

```js
module.exports = {
  "arrowParens": "avoid",
  "printWidth": 100,
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "none"
}
```
