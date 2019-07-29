  # Configurando projeto do zero

Vamos usar a CLI do react agora para criarmos nossos projetos. Para isso:

```
yarn create react-app nome
```

Criando dessa forma, tudo já vem configurado no webpack e babel.

Logo após a instalação, caso você utilize o eslint configurado por você mesmo, apague a parte do eslintConfig no package.json.

## Configurando ESLint, Prettier

Instale o eslint:

```
yarn add eslint -D
```

Execute no terminal:

```
yarn eslint --init
```

No terminal, selecione:

- Terceira opção
- Javascript Modules
- React
- Browser
- Use a popular StyleGuide
- Airbnb
- Javascript

### Agora vamos configurar e instalar o prettier

Para instalar o prettier e outras libs auxiliares:

```
yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -D
```

Agora no seu arquivo **.eslintrc**, faça as seguintes configurações:

```js
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: [
    'airbnb',
    // Adicione essas duas extensões
    'prettier',
    'prettier/react'
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  // Aqui também
  parser: 'babel-eslint',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: [
    'react',
    'prettier'
  ],
  rules: {
    // Adicione essas rules
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': [
      'warn',
      { extensions: ['.jsx', '.js'] }
    ],
    'import/prefer-default-export': 'off'
  },
};
```

Crie agora na raiz do seu projeto uma arquivo chamado **.prettierrc** com as seguintes configurações:

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

Pronto, o seu style guide está montado.
