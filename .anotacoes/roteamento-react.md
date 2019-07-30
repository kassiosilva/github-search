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

## Navegando entre páginas

A forma de navegação do react router é diferente da tradicional do navegador através dos links. Ele oferece um componente próprio, como se fosse uma tag "a" do html, e também oferece pelo próprio javascript.

```js
import { Link } from 'react-router-dom';

function Main() {
  return (
    <Link to="/repository">Detalhes</Link>
  )
}
```

**to**

- Serve como o atributo href da tag "a", recebe a rota a ser acessada.

### Recebendo parâmetros via url

```js
import { Link } from 'react-router-dom';

function Main() {
  return (
    <Link to={`/repository/${encodeURIComponent(repository.name)}`}>
      Detalhes
    </Link>
  )
}
```

- Perceba que passamos a informação repository.name pela url, porém esse parâmentro tem um caractere especial que no casso é a "/". Ao ver essa url, ela ficaria dessa forma:

```
/repository/kassiosilva/list-app
```

- Sabemos que tudo que vem precedido com uma "/" em uma url significa um novo caminho, diretório...
Queremos que essa barra não seja tratada assim, mas como parte do dado que estamos enviando, por isso usamos a função do javascript **encodeURIComponent** que serve para transforma esses caracteres da url em um caractere especial.

Também precisamos indicar na definição da rota que ela irá receber um parâmetro.

```js
// routes.js
export default function Routes() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/repository/:repository" component={Repository} />
      </Switch>
    </BrowserRouter>
  );
}
```

- Passamos uma barra com ":" para indicar o nome do parâmetro.

Para vermos se tudo está funcionando:

```js
// Repository/index.js
import React from 'react';

function Repository({ match }) {
  return <h1>Repository: {decodeURIComponent(match.params.repository)}</h1>;
}

export default Repository;
```

- Todos os parâmetro vindos via url, são guardados na prop chamado **match** e para acessá-las precisamos acessar o objeto **params**.
