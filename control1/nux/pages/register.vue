<template>
    <div class="container">
        <h1>Registrarse</h1>
        <form>
            <div class="form-item">
                <label for="nombre">Nombre</label>
                <input type="text" id="name" v-model="voluntario.nombre">
            </div>
            <div class="form-item">
                <label for="correo">Correo</label>
                <input type="text" id="correo" v-model="voluntario.correo">
            </div>
            <div class="form-item">
                <label for="ubicacion">Contraseña</label>
                <input type="text" id="contrasenia" v-model="voluntario.contrasenia">
            </div>
            <div>
                <button type="button" @click="register" class="main">Registrarse</button>
            </div>
        </form>
    
    </div>
    </template>
    <script>
    export default {
        data(){
            return{
                message:'',
                voluntario:{}
            }
        },
        methods:{
            register:async function(){
                this.message = '';
                //validaciones de formulario
                if (this.voluntario.nombre == ''||this.voluntario.correo==''||this.voluntario.contrasenia==''){
                    this.message = 'Debes ingresar todos los datos'
                    return false
                }
                //envío de datos del formulario
                try {
                    var result = await this.$axios.post('/voluntario/', this.voluntario);
                    this.message = `Se creó un nuevo voluntario`;
                } catch (error) {
                    //mensaje de error
                    console.log('error', error)
                    this.message = 'Ocurrió un error'
                }
            }
        }
    }
    </script>
    <style>
    code{
        padding: .5rem 1rem;
        color:white;
        background:#444;
        font-size: 1rem;
        width: 100%;
        display:inline-block;
    }
    p.message{
        border:solid 1px rgba(255, 255, 255, 0.25);
        padding: .5rem 1rem;
        font-weight: bold;
    }
    </style>