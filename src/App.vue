<template>
  <div id="app" class="container">
    <h1>Componentes Dinâmicos</h1>
    <button @click="componentSelecionado = 'Home'">Home</button>
    <button @click="componentSelecionado = 'PostLista'">Posts</button>
    <button @click="componentSelecionado = 'Sobre'">Sobre</button>
    <button @click="componentSelecionado = 'Assincrono'">Assincrono</button>
    <button @click="componentSelecionado = 'Contato'">Contato</button>

    <keep-alive include="Sobre">
      <component :is="componentSelecionado" v-bind="propsAtuais"></component>
    </keep-alive>
  </div>
</template>

<script>
import PostLista from "./components/PostLista.vue";
import Sobre from "./components/Sobre.vue";
import Home from "./components/Home.vue";

const Contato ={
  render: h=>h({
    name:'ContatoDados',
    template: '<h2>Component anonimo</h2>'
  })
}

export default {
  components: {
    Assincrono: () => ({
      component: new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(import("./components/Assincrono.vue"))

         //forçando dar o erro
         //reject("Carregamento Falhou")
        },2000);
      }),
      loading: { template: "<p>Carregando..</p>" },
      error: { template: "<p>Erro ao carregar component!</p>" },
      delay: 200,
      timeout: 3000
    }),
    Home,
    PostLista,
    Sobre,
    Contato
  },
  data() {
    return {
      componentSelecionado: "Home",
      posts: [
        {
          id: 1,
          titulo: "Componentes no Vue",
          conteudo: "Componentes são uma das peças mais importantes",
          autor: "Zezinho"
        },
        {
          id: 2,
          titulo: "Distribuindo conteudo com Slots",
          conteudo: "Slots podem ser usados como repositorios",
          autor: "Fábio Gonçalves"
        }
      ]
    };
  },
  computed: {
    propsAtuais() {
      return this.componentSelecionado === "PostLista"
        ? { posts: this.posts }
        : {};
    }
  }
};
</script>

<style scoped>
.container {
  width: 660px;
  margin: auto;
}
</style>
