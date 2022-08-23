<template>

  <div> 

  <div class="container mt-5" id="form">

    <h3>Ingresar salarios</h3>
    <div id="ingresars" class="d-flex justify-content-around">

    <input type="number" class="form-control my-3" v-model="nuevasPrestaciones" placeholder="Ingrese el sueldo aqui"> 
    <br>
    <input type="number" class="form-control my-3" v-model="nuevoComisionado"  placeholder="Ingrese las comisiones aqui">

    </div>
    <button class="btn btn-primary" @click="prestacion">Agregar</button>
  

    <div class="mt-4" v-for="item of prestaciones" v-bind:key="item">
      <div class="alert alert-primary" role="alert">
        <div class="d-flex justify-content-evenly">
          <div>
            <p>Salario:{{ item.salariomensual }}</p>  
          </div>
          <div>
            <p> Comision:{{ item.comisionmensual }}</p>
          </div>
          <div>
             <p> total:{{ item.totalidad }}</p>
          </div>
        </div>
      </div>
      

    </div>
       
    <div id="porcentajes" class="container d-flex justify-content-evenly">
      <p>Sumatoria de los salarios: {{todosumado}}</p>
      <p>Salario promedio Mensual: {{todopromedio}}</p>
      <p>Salario promedio Diario: {{tododiario}}</p>
    </div>
    <div class="container" id="validaciones">
      <div class="">
        <div>
        <p><input type="radio"  value="preaviso" v-model="preaviso"> Ha sido usted preavisado?{{preavisado}}</p>
          <p>{{spreaviso}}</p>
        </div>
        <div>
        <p><input type="radio"  value="cesantia" v-model="cesantia"> Desea agregar cesantia?{{cesantia}}</p>
        <p>{{scesantia}}</p>
        </div>
        <div>
        <p><input type="radio"  value="vacaciones" v-model="vacaciones"> Ha tomado vacaciones del año?{{vacaciones}}</p>
        <p>{{svacaciones}}</p>
        </div>
        <div>
        <p><input type="radio"  value="navidad" v-model="navidad"> Desea incluir salario de navidad?{{navidad}}</p>
          <p>{{snavidad}}</p>
        </div>


        
      </div>

    </div>
 
      
  </div>
</div>


</template>
<script>
export default {
  name: 'PriMer',
  data () {
    return {
      prestaciones: [],
      nuevasPrestaciones: '',
      nuevoComisionado: '',
      nuevaTotalidad: '',
      todosumado: 412000,
      todopromedio: null,
      tododiario: null,
      preavisado: null,
      cesantia: null,
      vacaciones: null,
      navidad: null,
      spreaviso: null,
      snavidad: null,
      scesantia: null,
      svacaciones: null,
      tsumado: []

    }
  },
  methods: {
      prestacion (){
          this.nuevaTotalidad = Number(this.nuevasPrestaciones) + Number(this.nuevoComisionado)
           if(this.prestaciones.length == 12){
            return;
          }
          this.prestaciones.push({
          salariomensual: this.nuevasPrestaciones,
          comisionmensual: this.nuevoComisionado,
          totalidad: this.nuevaTotalidad
        })


         

          console.log(this.prestaciones)

         this.todopromedio = (Math.trunc(this.todosumado) / (this.prestaciones.length)).toFixed()
         this.tododiario = ((this.todopromedio) / (30)).toFixed()
         
        this.nuevasPrestaciones = '',
        this.nuevoComisionado = '',
        this.nuevaTotalidad = '' 

        
  
  
        


        

      }
    }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: 0;
  margin: 0 10px;
}
a {
  color: #42b983;
}

p {
  list-style-type: none;
  padding: 0;
  display: inline-block;
  margin: 0 10px;
}

#porcentajes {
  font-size: 15px;
  padding: 15px;
  border-radius: 20px;
  background-color: #42b983;
  text-align: center;
  margin-top: 20px;
  margin: 15px;
}
#ingresar {
  padding: 10px;
}
</style>
