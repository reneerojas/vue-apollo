# Estado Local

Se você precisar gerenciar dados locais, poderá fazer com o  [apollo-link-state](https://github.com/apollographql/apollo-link-state) e a diretiva `@client`:

```js
export default {
  apollo: {
    hello: gql`
      query {
        hello @client {
          msg
        }
      }
    `
  },
  mounted () {
    // mutate the hello message
    this.$apollo
      .mutate({
        mutation: gql`
          mutation($msg: String!) {
            updateHello(message: $msg) @client
          }
        `,
        variables: {
          msg: 'hello from link-state!'
        }
      })
  }
}
```

Essa é uma maneira cada vez mais popular de gerenciar o estado do lado do cliente. Alguns projetos até usam isso como um substituto do Vuex (ou outras soluções inspiradas no Flux).

## Examplos

- [Example project](https://codesandbox.io/s/zqqj82396p) (by @chriswingler)
- [Todo App](https://codesandbox.io/s/x2jr96r8pp) (by @NikkitaFTW)
- [Todo App - Expanded](https://codesandbox.io/s/k3621oko23) (by @ScottMolinari fork of @NikkitaFTW's)

---
