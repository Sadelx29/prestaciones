<template>

  <div> 
    <div class="container">
        <div class="card" style="width: 100%rem;">
     <div  class="container d-flex justify-content-evenly">
        <div id="calendario">
         <h4>Datos del solicitante</h4>
         <div id="intro">
         <p>Cedula<input class="border-bottom" type="number"></p>
         <p>Nombre<input class="border-bottom" type="text" name="" id=""></p>
         <p>Empresa<input class="border-bottom" type="text"></p>
         </div>

            <h4>Seleccione las fechas</h4>
            <input type="date" class="border-bottom" v-model="fecha1">
        
            <input type="date" class="border-bottom" v-model="fecha2">

            
             
            

        </div>
        <div id="tipodecalculo" class="col-6">
            <ul id="picker">
                <h4>Seleccione el tipo de calculo</h4>
             <li>
                 <input type="radio" value=23.83 v-model="tipodecalculo">
                 <label for=23.83>Ordinario</label>

                <input type="radio" value=26 v-model="tipodecalculo">
                <label for=26>Intermitente</label>
            </li>
            <br>
            <div id="texto" class="">
            <li>
                <p>Condicion: {{condicion}}</p>
                <p>Ordinario: Jornada ordinaria es la ejecutada por trabajadores dentro de un período que no exceda de ocho (8) horas al día ni de cuarenta y cuatro (44) a la semana</p>
                <p>Intermitente: Jornada intermitente es la ejecutada por trabajadores que requieren su sola presencia en el lugar de trabajo, los cuales pudieran laborar consecuentemente por un periodo de hasta diez (10) horas diarias. Estos trabajadores son: los porteros, los ascensoristas, los serenos, los guardianes, los conserjes, los barberos, los sastres, los empleados de bombas para el expendio de gasolina, los capataces, los mozos de cafés y restaurantes, las manicuristas, los camareros, los trabajadores ocupados en vehículos de transporte terrestre que presten servicios intermitentes o entre dos o más municipios y los trabajadores del campo.
                Referencias: resolución 04/93 del Ministerio de Trabajo, sobre trabajadores que ejecutan labores intermitentes, arts. 281, 284 y 285 del Código de Trabajo y art. 78 del Reglamento 258/93 para la aplicación del Código de Trabajo.   </p>
                
            </li>
            </div>
            
            </ul>
            
        </div>
        </div>
        
       
    </div>
 
     <p></p>
  
</div>

  <div class="container mt-5" id="form">

    <h3>Ingresar salarios</h3>
    <br>
     <button class="btn btn-primary" @click="prestacion">Agregar</button>

    <div id="ingresars" class="d-flex justify-content-around">
    <input type="number" class="form-control my-3" v-model="nuevasPrestaciones" placeholder="Ingrese el sueldo aqui"> 
    <br>
    <input type="number" class="form-control my-3" v-model="nuevoComisionado"  placeholder="Ingrese las comisiones aqui">
      <div id="porcentajes" class="container d-flex justify-content-evenly">
      <p>Sumatoria de los salarios: {{todosumado}}</p>
      <br>
      <p>Salario promedio Mensual: {{todopromedio}}</p>
      <br>
      <p>Salario  Diario: {{tododiario}}  </p>
      <br>
    </div>
    
    
    
    </div>
          <div class="container " id="validaciones">
      <div class="">
        <div>
        <p><input type="radio"  value="si" v-model="preaviso"> Ha sido usted preaviso?{{preaviso}}</p>
          <p>{{spreaviso}}</p>
        </div>
        <div>
        <p><input type="radio"  value="si" v-model="cesantia"> Desea agregar cesantia?{{cesantia}}</p>
        <p>{{scesantia}}</p>
        </div>
        <div>
        <p><input type="radio"  value="si" v-model="vacaciones"> Ha tomado vacaciones del año?{{vacaciones}}</p>
        <p>{{svacaciones}}</p>
        </div>
        <div>
        <p><input type="radio"  value="si" v-model="navidad"> Desea incluir salario de navidad?{{navidad}}</p>
          <p>{{snavidad}}</p>
        </div>
      </div>
       <button type="button" class="btn btn-primary" @click="calcular">Calcular</button>
    </div>
       
       
    
    
    <div id="finales"></div>
        <div id="fecha"  style="width: 300px;">
              <p>Tiempo Laborado Años:{{tiempo}} Meses:{{month}} Dias:{{days}}</p>
            </div>
            <div id="fecha"  style="width: 300px;">
              <p>Total a recibir: {{totalrecibir}}</p>
            </div>
    </div>
    
     

  
   
  
      <div id="iteracion">
      
     <div class="mt-4 col-6" id="meses" v-for="item of prestaciones" v-bind:key="item">
      <div class="alert alert-primary" role="alert">
        <div id="mese" class="d-flex justify-content-evenly">
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
      todosumado: null,
      todopromedio: null,
      tododiario: null,
      preaviso: null,
      cesantia: null,
      vacaciones: null,
      navidad: null,
      spreaviso: null,
      snavidad: null,
      scesantia: null,
      svacaciones: null,
      tsumado: [],
      tipodecalculo: null,
      respuesta: '',
      fecha1: null,
      fecha2: null,
      tiempo: null,
      month: null,
      days: null,
      condicion: '',
      ordinario: 23.83,
      intermitente: 26,
      totalrecibir: null

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

        console.log(this.nuevaTotalidad, 'soy totalidad')

        const sumWithInitial = this.prestaciones.reduce(
        (nuevaTotalidad, currentValue) => nuevaTotalidad + currentValue.totalidad,
          0
        );
        this.todosumado = sumWithInitial

        console.log(this.prestaciones)

        console.log(this.prestaciones.length,'soy el ultimo')

        this.todopromedio = (Math.trunc(this.todosumado) / (this.prestaciones.length)).toFixed()
        this.tododiario = ((this.todopromedio) / (30)).toFixed()
         
        this.nuevasPrestaciones = '',
        this.nuevoComisionado = '',
        this.nuevaTotalidad = '' 
        

      },
       calcular(){

        // console.log(this.intermitente, 'intermitente')
        // console.log(this.ordinario,'ordinario')
        // 
        // console.log(this.tipodecalculo)
        // console.log(this.respuesta)
        // console.log(this.fecha1)
        // console.log(this.condicion, 'soy condicion')

        const fecha2 = new Date()
        const anoactual = parseInt(fecha2.getFullYear());
        const mesactual = parseInt(fecha2.getMonth()+1);
        const diaactual = parseInt(fecha2.getDate());
        const anoinicial=parseInt(String(this.fecha1).substring(0,4))
        const mesinicial=parseInt(String(this.fecha1).substring(5,7))
        const diainicial=parseInt(String(this.fecha1).substring(8,10))
        let ano = anoactual - anoinicial;
        let mes = mesactual - mesinicial;
        let dias = diaactual - diainicial;
        if (mesactual < mesinicial){
            ano--;
        }else if(mesactual === mesinicial){
            if(diaactual < diainicial){
                ano--; //
            }
        }
        if (ano <= 0){
            ano = 0
        }
        if (mes <= 0){
            mes = 0
        }
        if (dias <= 0){
            dias = 0
        }
        console.log(this.fecha2)
        this.tiempo = ano
        this.month = mes
        this.days = dias
        console.log(ano,mes,dias)

        console.log(this.tipodecalculo, 'soy tipo')

        this.totalrecibir =  this.snavidad + this.svacaciones + this.scesantia + this.spreaviso



        //CALCULO DE PREAVISO

        if(mes >= 3){
          
          console.log('3 meses multiplicar por 7', (this.tipodecalculo))
          this.spreaviso = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso / this.tipodecalculo))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso * 7))
        } 
        if(mes >= 6){
          console.log('6 meses se multiplica por catorce',(this.tipodecalculo))
          this.spreaviso = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso / this.tipodecalculo))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso * 14))
        }
        if(ano >= 1){
          
          console.log('un año se multiplica por 28',(this.tipodecalculo))
          this.spreaviso = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso / this.tipodecalculo))
          console.log(this.spreaviso)
          this.spreaviso = (Math.trunc(this.spreaviso * 28))
        }
         console.log(this.preaviso, 'soy preaviso')
         if(this.preaviso === 'si'){
           return  this.preaviso
         } else{
           this.spreaviso =  0
         }

        

        
       
        //  if(ano >= 1){
          
        //    console.log('1 año multiplicar por 14', (this.tipodecalculo))
        //    this.svacaciones = (Math.trunc(ultimomes / this.tipodecalculo))
        //    console.log(this.svacaciones)
        //    this.svacaciones = (Math.trunc(this.svacaciones / this.tipodecalculo))
        //    console.log(this.svacaciones)
        //    this.svacaciones = (Math.trunc(this.svacaciones * 6))
        //  } 
        // if(ano >= 5){
        //   console.log('5 años se multiplica por 18',(this.tipodecalculo))
        //   this.svacaciones = (Math.trunc(this.todosumado / this.prestaciones.length))
        //   console.log(this.scesantia)
        //   this.svacaciones = (Math.trunc(this.svacaciones / this.tipodecalculo))
        //   console.log(this.scesantia)
        //   this.svacaciones = (Math.trunc(this.svacaciones * 13))
        // }



         //CALCULO DE CESANTIA
        
        
        console.log(this.scesantia)

        if(mes >= 3){
          
          console.log('3 meses multiplicar por 6', (this.tipodecalculo))
          this.scesantia = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia / this.tipodecalculo))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia * 6))
        } 
        if(mes >= 6){
          console.log('6 meses se multiplica por 13',(this.tipodecalculo))
          this.scesantia = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia / this.tipodecalculo))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia * 13))
        }
        if(ano >= 1){
          
          console.log('un año se multiplica por 21',(this.tipodecalculo))
          this.scesantia = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia / this.tipodecalculo))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia * 21))
        }
        if (ano >= 5){

          console.log('cinco año se multiplica por 23',(this.tipodecalculo))
          this.scesantia = (Math.trunc(this.todosumado / this.prestaciones.length))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia / this.tipodecalculo))
          console.log(this.scesantia)
          this.scesantia = (Math.trunc(this.scesantia * 21))
        }
        

        console.log(this.cesantia, 'soy cesantia') 
        if(this.cesantia === 'si'){
          return this.cesantia
        } else{
          this.scesantia =  0
        }

        //CALCULO DE VACACIONES
        //this.vacaciones = ''
        console.log(this.vacaciones, 'soy vacaciones')
        this.svacaciones =  2 
        if(this.vacaciones === 'si'){
          return this.vacaciones
        } else{
          this.svacaciones =  0
        }
        
        console.log(this.vacaciones)

         //CALCULO DE NAVIDAD
        
        
          console.log(this.navidad, 'soy navidad') 
          this.snavidad = (Math.trunc(this.todosumado / this.prestaciones.length))


        if(this.navidad === 'si'){
          return this.snavidad
        } else {
          this.snavidad =  0
        }

        console.log(this.scesantia,this.spreaviso,this.snavidad,this.svacaciones, 'soy todo')



        // this.totalrecibir = (this.scesantia) + (this.spreaviso) + (this.svacaciones) + (this.snavidad)
        // console.log(this.totalrecibir, 'total recibir')

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

ul {
 list-style-type: none;
  padding: 10px;
  display: inline-block;
  margin: 10px;
}
li {
  list-style-type: none;
  padding: 2px;
  display: inline-block;
  margin: 10px;
}
#calendario input{
    margin: 10px;
}
#calendario input{
    border: 0ch;
}
#card{
    border: 0ch;
}
#picker label{
    padding: 10px;

}
#picker p{
    padding: 5px;

}
p {

  list-style-type: none;
  padding: 0;
  display: inline-block;
  margin: 0 10px;
}

#fecha {
  font-size: 15px;
  padding: 15px;
  border-radius: 20px;
  background-color: #42b983;
  text-align: center;
  margin-top: 20px;
  margin: 15px;
  text-align: center;
}
#texto {
  margin-bottom: 0 0px;
}
#intro input{
  border: 0ch;
}
#validaciones{
  text-align: right;
}

#btn {
  align-content: right;
}
#iteracione{
  align-content: left;
}

#finales{
  
}
</style>
