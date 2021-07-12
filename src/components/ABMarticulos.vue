<template>
    <div> 
        <hr>
        {{accionABM}} Articulos
        <div>
            <label>Nombre</label>
            <input type="text" v-model="datos.nombre">
        </div>
        <div>
            <label>Id</label>
            <input type="text" v-model="datos.id">
        </div>
        <div>
            <label>Codigo</label>
            <input type="text" v-model="datos.codigo">
        </div>
        <div>
            <label>Descripcion</label>
            <input type="text" v-model="datos.descripcion">
        </div>
        <div>
            <label>Cantidad</label>
            <input type="text" v-model="datos.cantidad">
        </div>
        <div>
            <label>Precio</label>
            <input type="text" v-model="datos.precio">
        </div>
        <div>
            <label>Fecha Vencimiento</label>
            <input type="datetime-local" v-model="datos.fecha_vencimiento">
        </div>
        <div>
            <label>Stock Minimo</label>
            <input type="text" v-model="datos.stock_min">
        </div>
        <div>
            <label>stock Maximo</label>
            <input type="text" v-model="datos.stock_max">
        </div>
        <div>
            <label>Rubro</label>
            <input type="text" v-model="datos.rubros_id">
        </div>
        <div>
            <button @click="funcAceptarr()"> Aceptar </button>
            |
            <button @click="funcCancelarr()"> Cancelar </button>
        </div>
        <!--<span>Ultimo Id {{ datos.id }}</span>-->
        <hr>
    </div>
</template>

<script>

import apiRest from "@/components/apiRest.vue"

export default {
    props: ['accionABM','idABM'],
    mixins: [apiRest],
    data() {
        return {
            datos: {
                id: 0,
                nombre: "",
                codigo: "",
                descripcion: "",
                cantidad: "",
                precio: "",
                fecha_vencimiento: "",
                stock_min: "",
                stock_max: "",
                rubros_id: "",
            }
        }
    },
    created() {
        console.log("evento created")
        if (this.accionABM != 'Ingresar') {
            this.funcObtenerDatosPorId('articulos', this.idABM)
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
        funcAceptarr() {
            if (this.accionABM == 'Ingresar') {
                this.funcInsertarDatos('articulos', this.datos)
                    .then(res => {
                        if (res.id != 0) {
                            console.log('El Articulo fue ingresado con exito')
                        } else {
                            console.log('Error al ingresar el Articulo')
                        }
                        this.$emit('SalirDeABMarticulos', true)
                    })
            }
            if (this.accionABM == 'Modificar') {
                this.funcEditarDatos('articulos', this.idABM, this.datos)
                    .then(res =>  {
                        this.datos = res
                        this.$emit('SalirDeABMarticulos', true)
                    })
            }
            if (this.accionABM == 'Eliminar') {
                this.funcEliminarDatos('articulos', this.idABM)
                    .then(res =>  {
                        this.datos = res
                        this.$emit('SalirDeABMarticulos', true)
                    })
            }
        },
        funcCancelarr() {
            this.$emit('SalirDeABMarticulos', false)
        }
    }
}
</script>