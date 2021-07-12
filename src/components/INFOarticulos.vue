<template>
    <div>
        <h1>Articulos </h1>
        <button
            @click="funcABMarticulos('Ingresar')" 
            class="btn btn-success"> Ingresar nuevo Articulo
        </button>
        <ABMarticulos 
            v-if="verABMarticulos"
            :accionABM=accionINFO
            :idABM=idINFO
            @SalirDeABMarticulos = funcMostrarABMarticulos($event)
        />
        <table class="table table-bordered">
        <thead>
            <tr class="columna_nombre">
            <th>
                Id
            </th>
            <th>
                Nombre_Articulo
            </th>
            <th>
                Codigo
            </th>
            <th>
                Descripcion
            </th>
            <th>
                Cantidad
            </th>
            <th>
                Precio
            </th>
            <th>
                Fecha de vencimiento
            </th>
            <th>
                Stock Minimo
            </th>
            <th>
                Stock Maximo
            </th>
            <th>
                rubros_id
            </th>
            <th>
                Acciones
            </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(articulos,item) in datos" :key="item">
            <td>
                {{articulos.id}}
            </td>
            <td>
                {{articulos.nombre}}
            </td>
            <td>
                {{articulos.codigo}}
            </td>
            <td>
                {{articulos.descripcion}}
            </td>
            <td>
                {{articulos.cantidad}}
            </td>
            <td>
                {{articulos.precio}}
            </td>
            <td>
                {{articulos.fecha_vencimiento}}
            </td>
            <td>
                {{articulos.stock_min}}
            </td>
            <td>
                {{articulos.stock_max}}
            </td>
            <td>
                {{articulos.rubro_id}}
            </td>
            <td>
                <button class="btn btn-warning" @click="funcABMarticulos('Modificar',articulos.id)" >
                    Modificar
                </button> 
                <button class="btn btn-danger" @click="funcABMarticulos('Eliminar',articulos.id)">
                    Eliminar
                </button> 
                <button class="btn btn-primary" @click="funcABMarticulos('Consultar',articulos.id)">
                    Consultar
                </button>
            </td>
            </tr>


        </tbody>
        </table>  
    </div>
</template>


<script>

import apiRest from "@/components/apiRest.vue"
import ABMarticulos from "@/components/ABMarticulos.vue"

export default {
    mixins: [apiRest],
    components: {ABMarticulos},
    data() {
        return {
            datos: [],
            verABMarticulos: false,
            accionINFO: '',
            idINFO: 0,
        } 
    },
    created() {
        console.log("evento created")
        this.funcTraerDatos()
    },
    mounted() {
        console.log("evento mounted")
        this.funcTraerDatos()
    },
    destroyed() {
        console.log("evento destroyed")
        this.funcTraerDatos()
    },
    methods: {
        funcABMarticulos(accion,id=0) {
            this.accionINFO = accion
            this.idINFO = id
            this.verABMarticulos = true

        },
        funcTraerDatos() {
            this.funcObtenerDatos('articulos')
                .then(res => {
                    this.datos = res
                }
            )
        },
        funcMostrarABMarticulos(ver) {
            this.verABMarticulos = false
            if (ver == true) {
                this.funcTraerDatos()
            }
        }
    }
}

</script>