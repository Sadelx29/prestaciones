<template>
    <div class="container">
        <div class="card" style="width: 100%rem;">
     <div  class="d-flex justify-content-around">
        <div id="calendario">
            <h4>Seleccione las fechas</h4>
            <input type="date" class="border-bottom" v-model="fecha1">
        
            <input type="date" class="border-bottom" v-model="fecha2">

             <div id="fecha" class="container d-flex justify-content-evenly">
                <p>Años:{{tiempo}}</p>
                <p>Meses:{{month}}</p>
                <p>Dias:{{days}}</p>
            </div>
            

        </div>
        <div id="tipodecalculo">
            <ul id="picker">
                <h4>Seleccione el tipo de calculo</h4>
             <li>
                 <input type="radio" id="yes" value="ordinario" v-model="tipodecalculo">
                 <label for="mensual">Ordinario</label>

                <input type="radio" id="no" value="intermitente" v-model="tipodecalculo">
                <label for="no">Intermitente</label>
            </li>
            <br>
            <li>
                <p>Condicion: {{condicion}}</p>
            </li>
            
            </ul>
            
        </div>
        </div>
        
       
    </div>
    <button type="button" class="btn btn-primary" @click="validar">Primary</button>
     <p>valor {{respuesta}}</p>
  
</div>
</template>
<script>
export default {
    name: 'ForM',
    data: function(){
        return{
            tipodecalculo: null,
            respuesta: '',
            fecha1: null,
            fecha2: null,
            tiempo: null,
            month: null,
            days: null,
            condicion: ''
        }
    },
    methods: {
       validar () {
        this.respuesta = Number(this.tipodecalculo) + Number(1)

        if(this.tipodecalculo === 'ordinario'){
           return this.condicion = 'Jornada ordinaria es la ejecutada por trabajadores dentro de un período que no exceda de ocho (8) horas al día ni de cuarenta y cuatro (44) a la semana'
        }
        if(this.tipodecalculo === 'intermitente'){
            return this.condicion = `Jornada intermitente es la ejecutada por trabajadores que requieren su sola presencia en el lugar de trabajo, los cuales pudieran laborar consecuentemente por un periodo de hasta diez (10) horas diarias. Estos trabajadores son: los porteros, los ascensoristas, los serenos, los guardianes, los conserjes, los barberos, los sastres, los empleados de bombas para el expendio de gasolina, los capataces, los mozos de cafés y restaurantes, las manicuristas, los camareros, los trabajadores ocupados en vehículos de transporte terrestre que presten servicios intermitentes o entre dos o más municipios y los trabajadores del campo.

        Referencias: resolución 04/93 del Ministerio de Trabajo, sobre trabajadores que ejecutan labores intermitentes, arts. 281, 284 y 285 del Código de Trabajo y art. 78 del Reglamento 258/93 para la aplicación del Código de Trabajo.   `
        }

        console.log(this.tipodecalculo)
        console.log(this.respuesta)
        console.log(this.fecha1)
        
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



       }
    }
}
</script>
<style scoped>
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
}
</style>