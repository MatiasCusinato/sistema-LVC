<template>
    <div> 
        <hr>
        {{ABMaccion}} Rubros
        <div>
            <label>Nombre</label>
            <input type="text" v-model="datos.nombre">
        </div>
        <div>
            <label>Id</label>
            <input type="text" v-model="datos.id" disabled>
        </div>
        <div>
            <button @click="funcAceptar()"> Aceptar </button>
            |
            <button @click="funcCancelar()"> Cancelar </button>
        </div>
        <!--<span>Ultimo Id {{ datos.id }}</span>-->
        <hr>
    </div>
</template>

<script>

import apiRest from "@/components/apiRest.vue"

export default {
    props: ['ABMaccion','ABMid'],
    mixins: [apiRest],
    data() {
        return {
            datos: {
                nombre: "",
                id: 0,
            }
        }
    },
    created() {
        console.log("evento created")
        if (this.ABMaccion != 'Ingresar') {
            this.funcObtenerDatosPorId('rubros', this.ABMid)
                .then(res => {
                    this.datos = res 
                })
        }
    },
    mounted() {
        console.log("evento mounted")
    },
    beforeDestroyed() {
        console.log("evento beforeDestroyed")
    },
    destroyed() {
        console.log("evento destroyed")
    },
    methods: {
        funcAceptar() {
            if (this.ABMaccion == 'Ingresar') {
                this.funcInsertarDatos('rubros', this.datos)
                    .then(res => {
                        if (res.id != 0) {
                            console.log('El registro fue ingresado con exito')
                        } else {
                            console.log('Error al ingresar el registro')
                        }
                        this.$emit('SalirDeABMrubros', true)
                    })
            }
            if (this.ABMaccion == 'Modificar') {
                this.funcEditarDatos('rubros', this.ABMid, this.datos)
                    .then(res =>  {
                        this.datos = res
                        this.$emit('SalirDeABMrubros', true)
                    })
            }
            if (this.ABMaccion == 'Eliminar') {
                this.funcEliminarDatos('rubros', this.ABMid)
                    .then(res =>  {
                        this.datos = res
                        this.$emit('SalirDeABMrubros', true)
                    })
            }
        },
        funcCancelar() {
            this.$emit('SalirDeABMrubros', false)
        }
    }
}
</script>