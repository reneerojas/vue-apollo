# Multiplos clientes

Você pode especificar vários clientes apollo caso seu aplicativo precise se conectar a diferentes endpoints do GraphQL:

```js
const defaultOptions = {
  // Você pode usar a `wss` para uma conexão segura (recomendado em produção)
  // Use `null` para desabilitar assinaturas
  wsEndpoint: process.env.VUE_APP_GRAPHQL_WS || 'ws://localhost:4000/graphql',
  // LocalStorage token
  tokenName: AUTH_TOKEN,
  // Ativar consulta automática persistindo com o mecanismo Apollo
  persisting: false,
  // Usar websockets para tudo (sem HTTP)
  // Você precisará passar um `wsEndpoint` para isso funcionar
  websocketsOnly: false,
  // Está sendo renderizado no servidor?
  ssr: false,
}

const clientAOptions = {
    // Você pode usar `https` para uma conexão segura (recomendado em produção)
    httpEndpoint: 'http://localhost:4000/graphql',
}

const clientBOptions = {
  httpEndpoint: 'http://example.org/graphql',
}

// Chame isso no arquivo do aplicativo Vue
export function createProvider (options = {}) {
  const createA= createApolloClient({
    ...defaultOptions,
    ...clientAOptions,
  });

  const createB = createApolloClient({
    ...defaultOptions,
    ...clientBptions,
  });

  const a = createA.apolloClient;
  const b = createB.apolloClient;

  // Crie o provedor do vue apollo
  const apolloProvider = new VueApollo({
    clients: {
      a,
      b
    }
    defaultClient: a,
})
```

Na opção `apollo` do componente, você pode definir o cliente para todas as consultas, assinaturas e mutações com
`$client` (apenas para esse componente):

```js
export default {
  apollo: {
    $client: 'b',
  },
}
```

Você também pode especificar o cliente em consultas individuais, assinaturas e mutações com a propriedade `client` nas opções:

```js
tags: {
  query: gql`...`,
  client: 'b',
}
```
