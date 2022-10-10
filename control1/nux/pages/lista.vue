<template>
    <div class="container">
    <h1>Todos las emergencias</h1>
    <ul class="item-list">
        <div class="container">
            <li class="" v-for="(item, index) in items" :key="index">
            <!-- <img :src="'https://loremflickr.com/160/120/dog?lock='+i"/>-->
                <!-- {{index}} -  -->
                <h2>ID: {{item.id}}</h2>
                <h2>Nombre: {{item.nombre}}</h2>
                <h2>Descripcion: {{item.descripcion}}</h2>
                <h2>Ubicacion: {{item.ubicacion}}</h2>
                <button v-on:click="verRequisitos(item.id)">Ver requisitos</button>
            </li>
            <li  v-for="(habilidad, index2) in habilidades" :key="index2">
                <h2>Nombre: {{habilidad.nombre}}</h2>
                <h2>Descripcion: {{habilidad.descripcion}}</h2>
                <input type="checkbox" id="habilidad" value="habilidad" v-model="habilidadesSeleccionadas">
            </li>
            <button class="agregar" v-on:click="agregarRequisitos()">Inscribirse</button>
        </div>
    </ul>
    <div v-if="items.length==0" class="empty-list">
      <em>No se han cargado los datos</em>
    </div>
  </div>
</template>
<script>
export default {
    //Función que contiene los datos del componente
    data(){
        return{
            //Lista de ítems a mostrar
            items:[],
            id:"",
            habilidades:[],
            habilidadesSeleccionadas:[]
        }
    },
    methods:{
        //Función asíncrona para consultar los datos
        getData: async function(){
            try {
                let response = await this.$axios.get('/emergencia/');
                this.items  = response.data;
            } catch (error) {
                console.log('error', error);
            }
        },
        actualizarId:function(id){
            this.id=id;
            this.borrar();
        },
        borrar:async function(){
            try {
                var result = await this.$axios.delete(`Delete/Emergencia/${this.id}`);
            } catch (error) {
                console.log('error', error)
                this.message = 'Ocurrió un error'
            }
        },
        verRequisitos:async function(id){
            try{
                console.log(id);
                var result = await this.$axios.get(`emergencia_habilidad/verRequisitos/${id}`);
                console.log(result.data);
                this.habilidades=result.data;
            }
            catch{
                console.log('error', error)
                this.message = 'Ocurrió un error'
            }
        },
        agregarRequisitos:async function(){
            console.log();
        }
    },
    //Función que se ejecuta al cargar el componente
    created:function(){
        this.getData();
    }
}
</script>
<style >
    .container{
        display: flex;
        flex-direction: column;
        height: 8rem;
    }
    .agregar{
        width: 8rem;
    }
</style>