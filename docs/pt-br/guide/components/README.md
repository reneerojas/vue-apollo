# O que são componentes Apollo?

Eles são componentes como quaisquer outros. Eles pegam um documento GraphQL em seu prop e usam o [scoped slot feature](https://vuejs.org/v2/guide/components-slots.html#Scoped-Slots) para enviar os resultados.

O benefício é que voce pode usar estes componentes diretamente no template ao invés de usar a opção `apollo` de seu componente. Em alguns casos você nem precisará adicionar a parte do script em seu `.vue`! Isto tudo é ainda mais declarativo.

Aqui um exemplo rápido de um [ApolloQuery](./query.md) em um template:

```vue
<template>
  <!-- Apollo Query -->
  <ApolloQuery :query="/* some query */">
    <!-- O resultado sera automaticamente atualizado -->
    <template slot-scope="{ result: { data, loading } }">
      <!-- Algum conteúdo -->
      <div v-if="loading">Loading...</div>
      <ul v-else>
        <li v-for="user of data.users" class="user">
          {{ user.name }}
        </li>
      </ul>
    </template>
  </ApolloQuery>
</template>

<!-- Não precisa do script -->
```

Olhe [ApolloQuery](./query.md) apara aprender como escrever consultas GraphQL no template.
