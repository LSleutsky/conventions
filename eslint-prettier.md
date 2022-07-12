## `ESLint`

The below is a configuration template for an `.eslintrc.json` file that has been used in a [Next.js](https://nextjs.org/) project with [TypeScript](https://www.typescriptlang.org/):

```json
"plugins": [
  "@typescript-eslint",
  "react",
  "@next/next",
  "simple-import-sort",
  "sort-keys-fix"
],
"extends": [
  "react-app",
  "eslint:recommended",
  "plugin:import/typescript",
  "plugin:react/recommended",
  "plugin:@typescript-eslint/recommended",
  "plugin:prettier/recommended",
  "plugin:@next/next/recommended"
],
"settings": {
  "react": {
    "version": "detect"
  }
},
"rules": {
  "@typescript-eslint/explicit-function-return-type": "off",
  "@typescript-eslint/explicit-module-boundary-types": "off",
  "@typescript-eslint/no-explicit-any": "off",
  "@typescript-eslint/no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
  "@typescript-eslint/padding-line-between-statements": [
    "error",
    {
      "blankLine": "always",
      "prev": "*",
      "next": [
        "class",
        "const",
        "debugger",
        "do",
        "exports",
        "for",
        "function",
        "if",
        "interface",
        "let",
        "multiline-const",
        "multiline-let",
        "return",
        "switch",
        "throw",
        "try",
        "type",
        "while"
      ]
    },
    {
      "blankLine": "always",
      "prev": [
        "case",
        "class",
        "const",
        "debugger",
        "do",
        "default",
        "for",
        "function",
        "if",
        "interface",
        "let",
        "multiline-const",
        "multiline-let",
        "switch",
        "try",
        "type",
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
      "prev": ["directive", "require"],
      "next": "*"
    },
    {
      "blankLine": "always",
      "prev": "*",
      "next": ["directive", "require"]
    },
    {
      "blankLine": "never",
      "prev": ["require"],
      "next": ["require"]
    },
    {
      "blankLine": "never",
      "prev": ["directive"],
      "next": ["directive"]
    }
  ],
  "import/export": "error",
  "import/newline-after-import": ["error", { "count": 1 }],
  "import/no-anonymous-default-export": "off",
  "import/no-duplicates": "error",
  "import/no-useless-path-segments": "error",
  "no-console": ["error", { "allow": ["error", "info"] }],
  "no-dupe-keys": "error",
  "no-duplicate-case": "error",
  "no-restricted-imports": ["error", { "patterns": ["../*"] }],
  "no-var": "error",
  "padding-line-between-statements": "off",
  "prefer-const": "error",
  "prettier/prettier": ["error", { "arrowParens": "avoid" }],
  "react/jsx-sort-props": ["error", {
    "ignoreCase": true,
    "reservedFirst": true
  }],
  "react/prop-types": "off",
  "react/react-in-jsx-scope": "off",
  "simple-import-sort/exports": "error",
  "simple-import-sort/imports": "error",
  "sort-keys-fix/sort-keys-fix": ["error", "asc", { "caseSensitive": false, "natural": true }],
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
    "files": ["*.js", "*.jsx", "*.ts", "*.tsx"],
    "rules": {
      "simple-import-sort/imports": [
        "error",
        {
          "groups": [
            ["^react$", "react-dom", "react-redux", "^redux", "^next"],
            ["^@", "^\\w"],
            ["^(types)(/.*|$)"],
            ["^(pages)(/.*|$)"],
            ["^(components)(/.*|$)"],
            ["^(styles)(/.*|$)"],
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
  }
]
```

## `Prettier`

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
