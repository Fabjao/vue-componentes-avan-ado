<template>
  <div>
    <h2>Sobre</h2>
    <p v-if="autor">Autor: {{autor}}</p>
    <input type="text" v-model="autor">
  </div>
</template>

<script>
export default {
  name:'SobreNos',
  data() {
    return { autor: "" };
  },
  created() {
    console.log("creada");
  },
  destroyed() {
    console.log("destruida");
  },
  activated(){
    console.log("activated")
  },
  deactivated(){
    console.log("deactivated")
  }

  
};
</script>
