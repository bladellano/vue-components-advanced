<template>

  <div id="app" class="container">

  <h1>Components Dinâmicos</h1>

  <button @click="componentSelected = 'Home'">Home</button>
  <button @click="componentSelected = 'PostsList'">Posts</button>
  <button @click="componentSelected = 'Sobre'">Sobre</button>
  <button @click="componentSelected = 'Assincrono'">Assincrono</button>
  <button @click="componentSelected = 'Contato'">Contato</button>

  <keep-alive :include="/Home|Sobre/">
  <!-- <keep-alive :exclude="['Home','PostsList']"> -->
  <!-- <keep-alive include="Sobre"> -->
    <component 
    :is="componentSelected"
    v-bind="currentProps"
    ></component>
  </keep-alive>

  </div>
</template>

<script>
import Home from './components/Home.vue'
import PostsList from './components/PostsList.vue'
import Sobre from './components/Sobre.vue'

const Contato = {
  render: (h) => h({
    name:'ContatoVue',
    template:'<h2>Component Anonimo</h2>'
  })
}

export default{
  components:{
    Assincrono: ()=>({
      // component: import('./components/Assincrono.vue'),
      component: new Promise((resolve, reject)=>{

        setTimeout(()=>{
            resolve(import('./components/Assincrono.vue'))
            // reject('Failure')
        },2000)

      }), 
      loading: {template:'<p>Carregando...</p>'},
      error: {template:'<p>Erro ao carregar o componente!</p>'},
      delay: 200,
      timeout: 3000
    }),
    Contato,
    Home,
    PostsList,
    Sobre
  },
  data(){
    return{
      componentSelected:'Home',
      posts:[
        {
          "id": 1,
          "title": "Tsunami atinge a costa do Japão",
          "content": "Um forte terremoto de magnitude 8,9 atingiu a costa do Japão na sexta-feira, gerando um tsunami que varreu cidades e causou danos em prédios e estradas.",
          "author": "BBC News"
        },
        {
          "id": 2,
          "title": "Vacina contra COVID-19 é aprovada para uso emergencial pela OMS",
          "content": "A Organização Mundial da Saúde (OMS) aprovou o uso emergencial da vacina contra COVID-19 desenvolvida pela Pfizer-BioNTech. A decisão permite que a vacina seja distribuída para países em todo o mundo que não têm acesso a vacinas.",
          "author": "CNN"
        }  
      ]
    }
  },
  computed:{
    currentProps(){
      return this.componentSelected === 'PostsList' 
      ? {posts: this.posts}
      : {}
    }
  }
}
</script>

<style scoped>
.container{
  width: 90%;
  margin: 0 auto;
  border: 1px dashed #333;
  padding: 4px;
  border-radius: 6px;
}

.post-paragraph{
  color: red;
}
</style>
