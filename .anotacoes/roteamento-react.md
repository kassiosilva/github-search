# Roteamento no React

> Não se esqueça! Com react, estamos contruindo um SPA, ou seja, as rotas servem para navegarmos entre páginas através da url, porém sem o carregamento nessa transição.

Para nos ajuadar nessa tarefa, vamos usar o **React router**, que serve para fazermos roteamento no front end:

```
yarn add react-router-dom
```

## Configurando um roteamento no react

Tudo no react é um componente, cada rota da aplicação é um componente.

```js
// routes.js
import React from 'react';
import { BrowserRouter, Switch, Route } from 'react-router-dom';

import Main from './pages/Main';
import Repository from './pages/Repository';

export default function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/" exact component={Main} />
        <Route path="/repository" component={Repository} />
      </Switch>
    </BrowserRouter>
  );
}
```

**BrowserRouter**

- Usado para o roteamento usando "/" na url, existem diversos tipos de navegação, mas o mais usar é esse.

- Esse componente dev está está recebendo todas as rotas da aplicação como filhos.

**Switch**

- Serve para chamar apenas uma rota por momento. O react router tem poder de chamar mais de uma rota, por isso utilizamos apenas o switch.

- Ele recebe todas as páginas da aplicação.

**Route**

- Cada Route representa uma página da aplicação. Esse componente recebe parâmetros, que são:

  - path : Aqui é definido a url para mostrar a página;
  - component: O componente que será exibido ao acessar essa rota;
  - exact: Trata a url como absoluta, ou seja, para acessar página a url definida precisa ser exatamente igual.

Depois configurar as rotas, exporte esse componente para o componente principal da aplicação.

```js
// App.js
import React from 'react';

import Routes from './routes';

function App() {
  return <Routes />;
}

export default App;
```

