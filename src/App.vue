<template>
  <div id="app">
    <Barlateral @select-quantity="chosenQuantity=$event"/>
    <!--Llama al componente Barlateral 
    e igual al compnente calculadora-->
    <Calculadora v-bind:physicalQuantity="chosenQuantity"/>
  </div>
</template>

<script>
import Barlateral from './components/Barlateral.vue'
import Calculadora from './components/Calculadora.vue'

export default {
   name: 'app',
    components: {  /* Estrae todo lo que esta dentro de los componentes */
    Barlateral,
    Calculadora
  },
  data: function(){
    return{
      chosenQuantity: {name:"Tiempo", id:2, units:["s","min","h"]} 
       /* the currently chosen quantity. Per default, the chosen quantity is TIME */
    }
  },
  methods:{
    /* ... */
  },
  computed: {
    getMeasure(){
      return this.quantities.find(x => x.name==this.chosenQuantity);
    }
  }
}

</script>

<style>
  body{
    margin:0;
    font-family:"Source Sans Pro";
  }
  #app{
    display:flex;
  }
</style>

