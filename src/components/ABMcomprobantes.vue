<template>
    <div> 
        <hr>
        {{ACCIONabm}} Comprobantes
        <div>
            <label>Id</label>
            <input type="text" v-model="datos.id">
        </div>
        <div>
            <label>Número de Comprobante</label>
            <input type="text" v-model="datos.num_comprobante">
        </div>
        <div>
            <label>Tipo de Operacion</label>
                <select name="tipo_operacion" 
                    v-model="datos.tipo_operacion">
                    <option value="1">Compra</option>
                    <option value="2">Venta</option>
                </select>
        </div>
        <div>
            <label>Fecha</label>
            <input type="datetime-local" v-model="datos.fecha">
        </div>
        <div v-for="(articulo, $id) in datos.PedirDatos" 
                        :key="$id">
                    <label> Articulos : </label>
                    <select name="datos.PedirDatos" v-model="datos.PedirDatos[$id].arti_id">
                        <option v-for="(articulo, $arti_id) in articulos" 
                            :key="$arti_id"
                            :value="articulos.id">
                                {{articulos.id}} | {{articulos.nombre}}
                        </option>
                    </select>             
                    <br>   
                    <label> Cantidad : </label>
                    <input type="number" name="datos.PedirDatos"
                        v-model="datos.PedirDatos[$id].arti_cantidad">   
                        <br>
                </div>
        <div>
            <table>
                    <tbody>
                        <tr v-for="(renglon, indice) in comprobanteRenglons" :key="indice">
                            <td>{{renglon.id}}</td>
                            <td>{{renglon.num_comprobante}}</td>
                            <td>{{renglon.fecha}}</td>
                            <td>{{renglon.tipo_operacion}}</td>
                            <td>{{renglon.nombre_articulo}}</td>
                            <td>{{renglon.cantidad}}</td>
                        </tr>
                    </tbody>
            </table>
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
    props: ['ACCIONabm','IDabm'],
    mixins: [apiRest],
    data() {
        return {
            datos: {
                id: 0,
                num_comprobante: "",
                fecha: "",
                tipo_operacion: {
                    1: "Compra",
                    2: "Venta",
                },
                PedirDatos:[
                    {  
                        arti_id:"0", 
                        arti_cantidad: "0",
                    },
                ],
                comprobanteRenglon: [],
                articulos: [],
            }
        }
    },
    created() {
        console.log("evento created")
        if (this.ACCIONabm != 'Ingresar') {
            this.funcObtenerDatosPorId('comprobante_cabeceras', this.IDabm)
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
            if (this.ACCIONabm == 'Ingresar') {
                this.funcInsertarDatos('comprobante_cabeceras', this.datos)
                    .then(res => {
                        if (res.id != 0) {
                            console.log('El Comprobante fue ingresado con exito')
                        } else {
                            console.log('Error al ingresar el Comprobante')
                        }
                        this.$emit('SalirDeABMcomprobantes', true)
                    })
            }
            if (this.ACCIONabm == 'Eliminar') {
                this.funcEliminarDatos('comprobante_cabeceras', this.IDabm)
                    .then(res =>  {
                        this.datos = res
                        this.$emit('SalirDeABMcomprobantes', true)
                    })
            }
        },
        funcCancelar() {
            this.$emit('SalirDeABMcomprobantes', false)
        },
        functraerArticulos(){
            this.funcObtenerDatos("articulos")
                .then(datos => {
                    this.articulos= datos
                })
        },
    },
}
</script>