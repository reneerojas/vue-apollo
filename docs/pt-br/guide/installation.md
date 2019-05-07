# Instalação

## Vue CLI Plugin

Eu criei um plugin para [vue-cli](http://cli.vuejs.org) entao você pode adicionar Apollo (com um servidor GraphQL opcional!) em literalmente dois minutos! ✨🚀

Em seu projeto vue-cli 3:

```bash
vue add apollo
```

Então você pode pularo para a próxima seção: [Basic Usage](./apollo/).

[More info](https://github.com/Akryum/vue-cli-plugin-apollo)

## Instalação manual

### 1. Apollo Client

Você pode usar tanto [Apollo Boost](#apollo-boost) ou [Apollo Client directly](#apollo-client-full-configuration) (mais trabalho de configuracao).

#### Apollo Boost

Apollo Boost é a maneira sem configuração para começar a user o Apollo Client. Este inclui alguns padrões, os quais recomendamos `InMemoryCache` e `HttpLink`, os quais vem configurados para você como recomendamos e são perfeitas para iniciar um desenvolvimento rápido.

Instale jonto com `vue-apollo` e `graphql`: 

```
npm install --save vue-apollo graphql apollo-boost
```

Ou:

```
yarn add vue-apollo graphql apollo-boost
```

Em seu app app, crie uma instância `ApolloClient`:

```js
import ApolloClient from 'apollo-boost'

const apolloClient = new ApolloClient({
  // Você deve usar uma URL absoluta aqui
  uri: 'https://api.graphcms.com/simple/v1/awesomeTalksClone'
})
```

#### Apollo client configuração completa

Se você quiser algum controlhe mais detalhado instale estes pacotes ao invés do apollo-boost:

```
npm install --save vue-apollo graphql apollo-client apollo-link apollo-link-http apollo-cache-inmemory graphql-tag
```

Ou:

```
yarn add vue-apollo graphql apollo-client apollo-link apollo-link-http apollo-cache-inmemory graphql-tag
```

Em seu app, crie uma instância `ApolloClient`:

```js
import { ApolloClient } from 'apollo-client'
import { createHttpLink } from 'apollo-link-http'
import { InMemoryCache } from 'apollo-cache-inmemory'

// HTTP conexão http como API
const httpLink = createHttpLink({
  // Você deve usa uma URL absoluta aqui
  uri: 'http://localhost:3020/graphql',
})

// implementação do Cache
const cache = new InMemoryCache()

// Crie o apollo client
const apolloClient = new ApolloClient({
  link: httpLink,
  cache,
})
```

### 2. Instale o plugin no Vue

```js
import Vue from 'vue'
import VueApollo from 'vue-apollo'

Vue.use(VueApollo)
```

### 3. Apollo provider

O provedor contem todas as intâncias do cliente Apollo que podem ser usadas por todos os componentes filhos.

```js
const apolloProvider = new VueApollo({
  defaultClient: apolloClient,
})
```

Adicione isso ao seu app com a opção `apolloProvider`:

```js
new Vue({
  el: '#app',
  // injete o apolloProvider aqui como o vue-router ou vuex
  apolloProvider,
  render: h => h(App),
})
```

Agora você está pronto para usar o Apollo em seus componentes!

## Integração IDE

### Visual Studio Code

Caso esteja usando VS Code, é recomendado que instale a [Apollo GraphQL extension](https://marketplace.visualstudio.com/items?itemName=apollographql.vscode-apollo).

Então configure criando o arquivo `apollo.config.js` na pasta raiz de seu projeto Vue:

```js
// apollo.config.js
module.exports = {
  client: {
    service: {
      name: 'my-app',
      // URL para o API GraphQL
      url: 'http://localhost:3000/graphql',
    },
  },
}
```
