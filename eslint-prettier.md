```js
// .eslintrc.json

"settings": {
    "react": {
      "version": "detect"
    }
  },
"rules": {
  "@typescript-eslint/explicit-function-return-type": "off",
  "@typescript-eslint/explicit-module-boundary-types": "off",
  "@typescript-eslint/no-explicit-any": "error",
  "@typescript-eslint/no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
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
  "padding-line-between-statements": [
    "error",
    {
      "blankLine": "always",
      "prev": "*",
      "next": [
        "cjs-export",
        "class",
        "const",
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
        "case",
        "class",
        "const",
        "debugger",
        "do",
        "directive",
        "default",
        "for",
        "function",
        "if",
        "let",
        "multiline-const",
        "multiline-let",
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
    }
  ],
  "prefer-const": "error",
  "prettier/prettier": ["error", { "arrowParens": "avoid" }],
  "react/prop-types": "off",
  "react/react-in-jsx-scope": "off",
  "simple-import-sort/exports": "error",
  "simple-import-sort/imports": "error",
  "sort-keys": ["error", "asc", { "caseSensitive": false, "minKeys": 2, "natural": true }]
},
"overrides": [
  {
    "files": ["*.js", "*.jsx", "*.ts", "*.tsx"],
    "rules": {
      "simple-import-sort/imports": [
        "error",
        {
          "groups": [
            ["^react", "^next"],
            ["^@?\\w"],
            ["^(api)(/.*|$)"],
            ["^(types)(/.*|$)"],
            ["^(context)(/.*|$)"],
            ["^(pages)(/.*|$)"],
            ["^(components)(/.*|$)"],
            ["^(styles)(/.*|$)"],
            ["^(config)(/.*|$)"],
            ["^(constants)(/.*|$)"],
            ["^(utils)(/.*|$)"],
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
