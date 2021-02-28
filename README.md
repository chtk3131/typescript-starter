# EditorConfigの設定
```
root = true

[*]
end_of_line = lf
charset = utf-8
insert_final_newline = true
trim_trailing_whitespace = true

[*.{json,scss,ts,tsx,yml}]
indent_style = space
indent_size = 2
```

# vscodeの設定
```
{
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  }
}
```

# TypeScriptインストール
## yarn
```
yarn add -D typescript ts-node
```
## tsconfig.jsonの設定
```
{
  "include": [
    "./src/**/*",
    "./gatsby-*.ts"
  ],
  "compilerOptions": {
    "target": "es2019",
    "module": "commonjs",
    "lib": ["dom", "es2017"],
    "jsx": "react",
    "strict": true,
    "esModuleInterop": true,
    "baseUrl": "."
  }
}
```

# ESLint・Pretter
## yarn
```
yarn add -D eslint prettier eslint-config-prettier eslint-plugin-import eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks @typescript-eslint/eslint-plugin @typescript-eslint/parser
```
## eslintrc.json
```
{
  "root": true,
  "extends": [
    "eslint:recommended",
    "plugin:import/errors",
    "plugin:import/warnings",
    "plugin:import/typescript",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended",
    "prettier/@typescript-eslint"
  ],
  "plugins": [
    "import",
    "react",
    "react-hooks",
    "@typescript-eslint",
    "prettier"
  ],
  "env": {
    "es6": true,
    "node": true,
    "browser": true
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "sourceType": "module",
    "project": "./tsconfig.json",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "rules": {
    "react/prop-types": "off",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "trailingComma": "none",
        "arrowParens": "avoid"
      }
    ]
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}
```
## eslintignore
```
package.json
package-lock.json
.cache/
public/
types/
```
## スクリプト実行用にpackage.jsonに追加
```
{
  // ...
  "scripts": {
    "lint": "eslint 'src/**/*.{ts,tsx}' gatsby-*.ts && tsc --noEmit",
    "lint:fix": "eslint --fix 'src/**/*.{ts,tsx}' gatsby-*.ts && tsc --noEmit"
  },
  // ...
}
```

# stylelint
## yarn
```
yarn add -D stylelint stylelint-prettier stylelint-config-prettier stylelint-scss stylelint-config-recommended-scss
```
## .stylelintrc.json
```
{
  "extends": [
    "stylelint-config-recommended-scss",
    "stylelint-prettier/recommended"
  ]
}
```
## スクリプト実行用にpackage.jsonに追加
```
{
  // ...
  "scripts": {
    // ...
    "stylelint": "stylelint 'src/**/*.scss'",
    "stylelint:fix": "stylelint --fix 'src/**/*.scss'"
  },
  // ...
}
```

# Gitフック
## yarn
```
yarn add -D husky lint-staged
```
## スクリプト実行用にpackage.json追加
```
{
  // ...
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged && tsc --noEmit"
    }
  },
  "lint-staged": {
    "*.{ts,tsx}": "eslint --fix",
    "*.scss": "stylelint --fix"
  },
  // ...
}
```

