<template>
  <article>
    <h2>{{ article.title }}</h2>
     <pre>{{ article.slug }}</pre>
    <h3>esto se actualizo  {{ formatDate(article.updatedAt) }}</h3>
    <!-- <pre> <code> {{ article }} </code> </pre> -->

    <h1>este h1 no es de l blog</h1>
    
    

    <nuxt-content :document="article" />
  </article>
</template>


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




<style>
    h1{
        color: blueviolet;
    }

    .nuxt-content h1{
      color: cadetblue;
    }
</style>
