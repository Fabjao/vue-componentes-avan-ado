<template>
  <div id="app" class="container">
    <h1>Componentes Dinâmicos</h1>
    <button @click="componentSelecionado = 'Home'">Home</button>
    <button @click="componentSelecionado = 'PostLista'">Posts</button>
    <button @click="componentSelecionado = 'Sobre'">Sobre</button>
    <p>{{componentSelecionado}}</p>

<component :is="componentSelecionado"></component>

  </div>
</template>

<script>
import PostLista from "./components/PostLista.vue";
import Sobre from "./components/Sobre.vue";
import Home from "./components/Home.vue";
export default {
  components: {
    Home,
    PostLista,
    Sobre
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
  }
};
</script>

<style scoped>
.container {
  width: 660px;
  margin: auto;
}
</style>
