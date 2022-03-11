# Como Surfear por nuestro blog 🏄

Bueno partamos de la base que ya tenemos nuestras paginas creadas a pelo o usando[componentes](./Componentes.md). Recuerda que las paginas las encontramos dentro de la carpeta ***pages***

ahora para movernos entre paginas como lo hacemos

Nuxt nos proporciona atraves de NuxtLink la misma funcionalidad con algunos extras pero vamos que con lo que te tienes que quedar es...

```html

<!-- ejemplo en html  -->

<a href="www.holaMundo.com">vamos a saludar el mundo</a>

<!-- ejemplo con nuxt -->

<NuxtLink to="www.holaMundo.com/nuxt">Vamos a saludar al mundo con nuxt</NuxtLink>

```

vale el concepto esta claro pero dame un ejemplo de como usarlo dentro del blog

```vue
<template>
  <main>
    <h1>Home page</h1>
    <NuxtLink to="/about">
      About (internal link that belongs to the Nuxt App)
    </NuxtLink>
    <a href="https://nuxtjs.org">External Link to another page</a>
  </main>
</template>

```

como vemos los enlaces internos del blog son gestionados con ***NuxtLink*** y cualquier cosa fuera de ella usaremos nuestro querido anchor de HTML <a>

## la docu oficial[↪️](https://nuxtjs.org/docs/get-started/routing)