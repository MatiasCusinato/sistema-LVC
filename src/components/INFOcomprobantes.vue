<template>
    <div>
        <h1> Comprobantes </h1>
        <button @click="funcABMcomprobantes('Ingresar')" class="btn btn-success"> Ingresar nuevo comprobante
        </button>
        <ABMcomprobantes 
            v-if="verABMcomprobantes == true"
            :ACCIONabm=infoACCION
            :IDabm=infoID
            @SalirDeABMcomprobantes = funcMostrarABMcomprobantes($event)
        />
        <table class="table table-bordered">
        <thead>
            <tr class="columna_nombre">
                <th>ID</th>
                <th>Número comprobante</th>
                <th>Tipo de Operacion</th>
                <th>Fecha</th>
                <th>Acciones</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(comprobante_cabeceras,item) in datos" :key="item">
            <td>
                {{comprobante_cabeceras.id}}
            </td>
            <td>
                {{comprobante_cabeceras.num_comprobante}}
            </td>
            <td>
                {{comprobante_cabeceras.tipo_operacion}}
            </td>
            <td>
                {{comprobante_cabeceras.fecha}}
            </td>
            <td>
                <button @click="funcABMcomprobantes('Eliminar', comprobante_cabeceras.id)" class="btn btn-danger">
                    Eliminar
                </button> |
                <button @click="funcABMcomprobantes('Consultar', comprobante_cabeceras.id)" class="btn btn-primary">
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
import ABMcomprobantes from "@/components/ABMcomprobantes.vue"

export default {
    mixins: [apiRest],
    components: {ABMcomprobantes},
    data() {
        return {
            datos: [],
            Renglons: [],
            verABMcomprobantes: false,
            infoACCION: '',
            infoID: 0,
        } 
    },
    created() {
        this.funcTraerDatos()
    },
    methods: {
        funcABMcomprobantes(accion,id=0) {
            this.infoACCION = accion
            this.infoID = id
            this.verABMcomprobantes = true

        },
        funcTraerDatos() {
            this.funcObtenerDatos('comprobante_cabeceras')
                .then(res => {
                    this.datos = res
                }
            )
        },
        funcMostrarABMcomprobantes(ver) {
            this.verABMcomprobantes = false
            if (ver == true) {
                this.funcTraerDatos()
            }
        }
    }
}
</script>