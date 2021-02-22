<template>
 <div id="nav">
     <div id="header">
       Calculadora De Unidades
       
    </div>
     <a v-for="quantity in quantities" v-bind:key="quantity.name" @click="$emit('select-quantity',quantity)" >
     {{quantity.name}}<!-- lista todas las cantidades y se emite un evento personalizado denominado 'select-cantidad'.-->  
     </a>
     <div id="footer">

     </div>
     
        
     
 </div>
</template>

<script>
export default {
  name:'Barlateral',
  data: function(){
      return{
          quantities: [  /* todas las cantidades físicas con las que estamos trabajando y sus respectivas unidades */ 
                      {name:"Longitud",id:0, units:["mm","cm","m","km","milla","yarda","pie","pulgada"]},
                      {name:"Temperatura",id:1, units:["C","K","F"]},
                      {name:"Tiempo",id:2, units:["s","min","h" ]},
                      {name:"Masa", id:3, units:["gramos","kilogramo","milligramo","libra","onza"]},
                      {name:"Almacenamiento", id:4, units:["megabyte","gigabyte","terabyte","petabyte"]},
                      {name:"Moneda", id:5, units:["dolar","peso_mexicano","euro"]}
                      ]
            }
       },
  methods:{
   /* ...... */
  }
}
</script>

<style scoped>
    #nav{
        display:flex;
        flex-direction:column;
        height:100vh;
        width:20vw;
        background-color:#024d9c;
        color:rgb(255, 255, 255);
    }
    #nav>div{
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        padding:20px 0 20px 0;
        text-align:Center;
        vertical-align:middle;
    }

    a{
       text-align:center;
       padding:20px;
       background-color:rgb(0, 0, 0);
       transition:background-color 0.5s;
       cursor:pointer;
    }
    a:hover{
        background-color:rgb(0, 0, 0);
    }
    #footer{
        height:15vh;
        background-color:#024d9c;
        margin-top:auto; 
        box-sizing:border-box;
        padding:15px;
        font-size:0.8em;
    }
</style>


