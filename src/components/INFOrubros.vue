<template>
    <div>
        <h1> Rubros </h1>
        <button @click="funcABMrubros('Ingresar')" class="btn btn-success"> 
            Ingresar nuevo Rubro
        </button>
        <ABMrubros 
            v-if="verABMrubros"
            :ABMaccion=INFOaccion
            :ABMid=INFOid
            @SalirDeABMrubros = funcMostrarABMrubros($event)
        />
        <table class="table table-bordered">
        <thead>
            <tr class="columna_nombre">
            <th>
                Id
            </th>
            <th>
                Nombre_Rubro
            </th>
            <th>
                Acciones
            </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(rubros,item) in datos" :key="item">
            <td>
                {{rubros.id}}
            </td>
            <td>
                {{rubros.nombre}}
            </td>
            <td>
                <button @click="funcABMrubros('Modificar', rubros.id)" class="btn btn-warning">
                    Modificar
                </button> |
                <button @click="funcABMrubros('Eliminar', rubros.id)" class="btn btn-danger">
                    Eliminar
                </button> |
                <button @click="funcABMrubros('Consultar', rubros.id)" class="btn btn-primary">
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
import ABMrubros from "@/components/ABMrubros.vue"

export default {
    mixins: [apiRest],
    components: {ABMrubros},
    data() {
        return {
            datos: [],
            verABMrubros: false,
            INFOaccion: '',
            INFOid: 0,
        } 
    },
    created() {
        this.funcTraerDatos()
    },
    methods: {
        funcABMrubros(accion,id=0) {
            this.INFOaccion = accion
            this.INFOid = id
            this.verABMrubros = true

        },
        funcTraerDatos() {
            this.funcObtenerDatos('rubros')
                .then(res => {
                    this.datos = res
                }
            )
        },
        funcMostrarABMrubros(ver) {
            this.verABMrubros = false
            if (ver == true) {
                this.funcTraerDatos()
            }
        }
    }
}
</script>