<template>
  <div id="container">

    <h1>{{physicalQuantity.name}}</h1>

    <div id="main">
        <input type="text" v-model="fromValue" placeholder="">
        <select v-model="fromUnit"> 
            <option v-for="unit in physicalQuantity.units" v-bind:key="unit"> {{unit}} </option>
        </select>
        <p id="result">
            {{result}}
        </p> 
        <select v-model="resultUnit" placeholder="result"> 
            <option v-for="unit in physicalQuantity.units" v-bind:key="unit"> {{unit}} </option>
        </select>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Calculadora',
  
  props: {
    physicalQuantity: Object  
  },
  data: function(){            
       return{
         fromValue:1,
         fromUnit:"",
         resultUnit:""
       }
  },
  methods:{
      
      toMinutes: function(value,unit){   // convierte un valor s, min,h
          switch(unit){
            case("s"):
                return value/60;
            case("min"):
                return value;
            case("h"):
                 return value*60;
            default:
                 console.log("error en la conversión toMinutes")
                 return value;
          }
      },
      toMeters: function(value,unit){   // convierte un valor en mm, cm, m
        switch(unit){
            case("mm"):
                return value/1000;
            case("cm"):
                return value/100;
            case("m"):
                return value;/**/ 
            case("km"):
                return value*1000;
            case("milla"):
                return value*1609;
            case("yarda"):
                return value/1.094;
            case("pie"):
                return value/3.281; 
            case("pulgada"):
                return value/39.37;  
            default:
                console.log("error en la conversión toMeters")
                return value;
        }
      },
      toCelsius: function(value,unit){   // convierte un valor en C, F, K
        switch(unit){
            case("C"):
                return value;
            case("F"):
                return (value-32)*5/9;
            case("K"):
                return value-273.15;
            default:
                console.log("error en la conversión deCelsius")
                return value;
        }
      },
       toMasa: function(value,unit){   // convierte un valor
        switch(unit){
            case("gramos"):
                return value;       
            case("kilogramo"):
                return value*1000;
            case("milligramo"):
                return value/1000;
            case("libra"):
                return value*454;
            case("onza"):
                return value*28.35;
            default:
                console.log("error en la conversión deMasa")
                return value;
        }
      },
       toAlmacenamiento: function(value,unit){   // convierte un valor
        switch(unit){
            case("megabyte"):
                return value;       
            case("gigabyte"):
                return value*1000;
            case("terabyte"):
                return value*1000;
            case("petabyte"):
                return value*1000;
            default:
                console.log("error en la conversión de toAlmacenamiento")
                return value;
        }
      },
      toMoneda: function(value,unit){   // convierte un valor
        switch(unit){
            case("dolar"):
                return value;       
            case("peso_mexicano"):
                return value/20.4276;
            case("euro"):
                return value/0.83;
            default:
                console.log("error en la conversión de toAlmacenamiento")
                return value;
        }
      }
  },
  computed: {           
      result: function(){
            let value = parseFloat(this.fromValue); 
            if(isFinite(value)){                         
              switch(this.physicalQuantity.name){  
                   /*-----------------------------*/
                case("Tiempo"): {
                    /* ------------Calcular El Tiempo-------------*/
                        let valueInMinutes = this.toMinutes(value,this.fromUnit);  // usamos minutes, meters celsius como unidad intermediaria
                        switch(this.resultUnit){
                        case("s"):/*----------segundos----------*/
                            return parseFloat((valueInMinutes*60).toFixed(5));   // limitar a  5 decimales
                        case("min"):/*----------minutos----------*/
                            return parseFloat((valueInMinutes).toFixed(5));
                        case("h"):/*----------horas----------*/
                            return parseFloat((valueInMinutes/60).toFixed(5));
                        default:
                            console.log("Error al calcular el tiempo");
                            return "...";
                         }
                }
                  /* ----------------------------*/
                 case("Longitud"): {
                    /* ------------Calcular la Longitud-------------*/
                        let valueInMeters= this.toMeters(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("mm"):/*----------milimetros----------*/
                            return parseFloat((valueInMeters*1000).toFixed(5));   
                        case("cm"):/*---------centrimetros----------*/
                            return parseFloat((valueInMeters*100).toFixed(5));
                        case("m"):/*----------metros----------*/
                            return parseFloat((valueInMeters).toFixed(5));
                        case("km"):/*----------kilometros----------*/
                            return parseFloat((valueInMeters/1000).toFixed(5));
                        case("milla"):/*----------milla----------*/
                            return parseFloat((valueInMeters/1609).toFixed(5));
                        case("yarda"):/*----------yarda----------*/
                            return parseFloat((valueInMeters*1.094).toFixed(5));
                        case("pie"):/*----------pie----------*/
                            return parseFloat((valueInMeters*3.281).toFixed(5));
                        case("pulgada"):/*----------pulgada----------*/
                            return parseFloat((valueInMeters*39.37).toFixed(5));
                        default:
                            console.log("Error al calcular la Longitud");
                            return "...";
                        }
                    /*--------------------------- */
                 }
                  /* ----------------------------*/
                  case("Temperatura"): {
                    /* ------Calcular la temperatura-------------*/
                        let valueInCelsius= this.toCelsius(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("C"):/*----------Celsius----------*/
                            return parseFloat((valueInCelsius).toFixed(5));   
                        case("K"):/*----------Kelvin----------*/
                            return parseFloat((valueInCelsius+273.15).toFixed(5));
                        case("F"):/*----------Fahrenheit----------*/
                            return parseFloat((valueInCelsius*1.8+32).toFixed(5));
                        default:
                            console.log("Error al calcular la temperatura");
                            return "...";
                        }
                  }
                  /* ----------------------------*/
                  case("Masa"): {
                    /* ------Calcular la Masa-------------*/
                        let valueInMasa= this.toMasa(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("gramos"):
                            return parseFloat((valueInMasa).toFixed(5))      
                        case("kilogramo"):
                            return parseFloat((valueInMasa/1000).toFixed(5));
                        case("milligramo"):
                            return parseFloat((valueInMasa*1000).toFixed(5));
                        case("libra"):
                            return parseFloat((valueInMasa/454).toFixed(5));
                        case("onza"):
                        return parseFloat((valueInMasa/28.35).toFixed(5));
                        default:
                            console.log("Error al calcular la masa");
                        return "...";
                        }
                  }
                   /* ----------------------------*/
                  case("Almacenamiento"): {
                    /* ------Calcular el Almacenamiento-------------*/
                        let valueInCAlmacenamiento= this.toAlmacenamiento(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("megabyte"):/*----------megabyte----------*/
                            return parseFloat((valueInCAlmacenamiento).toFixed(5));   
                        case("gigabyte"):/*----------gigabyte----------*/
                            return parseFloat((valueInCAlmacenamiento/1000).toFixed(5));
                        case("terabyte"):/*----------terabyte----------*/
                            return parseFloat((valueInCAlmacenamiento/1000).toFixed(5));
                         case("petabyte"):/*----------terabyte----------*/
                            return parseFloat((valueInCAlmacenamiento/1000).toFixed(5));
                        default:
                            console.log("Error al calcular la temperatura");
                            return "...";
                        }
                  }
                  /* ----------------------------*/
                  case("Moneda"): {
                    /* ------Calcular la temperatura-------------*/
                        let valueInMonedad= this.toMoneda(value,this.fromUnit);  
                        switch(this.resultUnit){
                        case("dolar"):/*----------dolar----------*/
                            return parseFloat((valueInMonedad).toFixed(5));   
                        case("peso_mexicano"):/*----------peso_mexicano----------*/
                            return parseFloat((valueInMonedad*20.4276).toFixed(5));
                        case("euro"):/*----------euro----------*/
                            return parseFloat((valueInMonedad*0.83).toFixed(5));
                        default:
                            console.log("Error al calcular la temperatura");
                            return "...";
                        }
                  }
              }  
            }      
            return "...";   // respuesta al no escribir un numero
      }
  }
}
</script>


<style scoped>
  #container{
    width:80vw;
    color:rgba(255, 255, 255, 0.61);
    height:100vh;
    display:flex;
    flex-direction:column;
    justify-content:flex-start;
  }
  h1{
    width:100%;
    background-color:rgb(0, 0, 0);
    box-sizing:border-box;
    padding:40px;
  }
  #main{
    display:flex;
    box-sizing:border-box;
    padding:40px;
  }
  
  #main>*{
    margin:0 5px 0 5px;
  }
  input,select,#result{
    padding:12px;
    border: 5px solid rgb(0, 255, 0);
    border-radius:10px;
    width:10vw;
    font-family:"Source Sans Pro";
    font-size:1em;
    display:flex;
    align-items:center;
  }
</style>