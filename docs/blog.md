# Vamos a empezar a crear los componentes del blog

pues hemos visto muchas cosas en el resto de la documentacion, pero creo que este proyecto era para que un profesor tuviera un blog para que pueda seguir compartiendo su conocimiento con todo el mundo

## hagamos un hola mundo blog

en este repo ya vas a tener creada la siguiente ruta

> content/articles

una de las razones para usar nuxt+content en este blog es que podemos usar de una manera muy sencilla archivos [markdown](https://markdown.es/) para crear nuestros posteos en el blog.

dentro de la ruta, creamos nuestro archivo *mi-primer-blog.md*

dentro podemos poner el siguiente codigo 

```md
# hola mundo

estamos creando nuestra primera entrada al blog
```

ok ahora vamos a crearnos un componente para manejar nuestros post

lo primero es crear una pagina dinamica, dentro de la siguiente ruta ▶️
>pages/blog

```Shell
#linux
touch _slug.vue

```
o ayudate del SO y crealo como una persona normal con boton derecho y crear archivo

### dentro de slug

primero veamos como es un archivo _slug.vue

```vue
<template>
// 1 ARTICLE 
  <article>
    <h2>{{ article.title }}</h2>
    <pre>{{ article.slug }}</pre>
    <h3>esto se actualizo  {{ formatDate(article.updatedAt) }}</h3>
    <pre>{{ article }}</pre>
    

    <nuxt-content :document="article" />
  </article>
</template>

// 2 SCRIPT
<script>
  export default {
    async asyncData({ $content, params }) {
      
        const article = await $content('articles' ,params.slug).fetch()

        return { article }
    },
    methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
 }
  }

</script>



// 3 STYLES
<style>
    h1{
        color: blueviolet;
    }
</style>

```

como hemos visto las paginas incluso las dinamicas empiezan con la etiqueta template pero vamos a ver lo interesante

#### 1. ARTICLES

dentro de las etiquetas ```<article>...</article>``` vamos a definir nuestra plantilla.

dentro podemos hacer la pagina igual que lo hariamos en HTML 😄

Sin embargo tenemos algo que no es nativo de HTML
```vue
<nuxt-content :document="article" />
```
esta etiqueta nos va a devolver el post que hemos escrito en markdown y lo va a mostrar en la pagina 

#### 2. SCRIPTS

Aqui dentro usaremos nuestros scripts, una funcion en concreto sera la que nos devuelva toda la informacion de los post creados

```javascript
export default {
    async asyncData({ $content, params }) {
      
        const article = await $content('articles' ,params.slug).fetch()

        return { article }
    }
```
esta funcion para resumirlo mucho va a buscar dentro de nuestro proyecto la carpeta ***articles*** y dentro de ***content*** que a su vez nuext utiliza como contenxto 😵

hay gente que lo llama magia 🪄 y si es magia la magia del framework.

esto nos da acceso dentro de usar la variable article para extraer informacion sobre el post mediante dobles llaves ***{{ }}***
```vue
<template>
  <h2>{{ article.title }}</h2>
    <pre>{{ article.slug }}</pre>
</template>
```

si queremos investigar 🔍 un poco lo que trae podemos imprimirlo bien o por consola dentro del script o en nuestra plantilla a traves ayudandonos de la etiqueta pre

```vue
<template>
    <pre>{{ article.slug }}</pre>
</template>
```

Ademas podemos usar nuestros metodos para ello nos creamos una una propiedad methods y le vamos agregando nuestras funciones

```vue
<script>

export default{

  methods: {
   formatDate(date) {
     const options = { year: 'numeric', month: 'long', day: 'numeric' }
     return new Date(date).toLocaleDateString('en', options)
   }
  }
}

</script>
```

#### 3. STYLES

Por ultimo los estilos aqui estaran los estilos especificos de los post. 

```vue
<style>
    h1{
        color: blueviolet;
    }
</style>
```

ok pero nostros escribimos nuestros post en markdown no?? :frowning:

sip, pero al renderizar la pagina hay una equivalencia entre el formato de md y el HTML.

por hacer una pequeña comparacion vamos a ver la siguiente tabla

| markdown      | HTML     |
| ------------ | -------- |
| #   | \<h1>\</h1>|
| ## | \<h2>\</h2> |
| espacio vacio | \<p>\</p> |


para mas informacion sobre las equivalencias  [:link:](https://www.markdownguide.org/basic-syntax/)

 y si solo queremos darle estilos a nuestras entradas del blog que hacemos??? :point_up: 

 para ello dentro podemos los estilos para la clase ***.nuxt-content*** y luego indicarle la etiqueta a la que le queremos apuntar

 ```css
 .nuxt-content h1{
   color: blue;
 }
 ```

## Parece que ya tenemos los basico
vamos a hacer un breve repaso

1. creamos un post dentro de nuesra carpeta articles que esta dentro de content
2. la mostramos dentro de una pagina dinamica
3. a molar 🚀

## por ultimo
una vez que tengamos un nuevo articulo o alguna modificacion lo unico que tendremos que hacer es un commit de nuestros cambios y un push al repo remoto para que se cree nuestra nueva entrada al blog o cualquier modificacion.







