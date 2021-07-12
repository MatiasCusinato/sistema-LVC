<template>
  <div class="home">
    <button @click="funcMostrarRubros()">Rubros</button>
    |
    <button @click="funcMostrarArticulos()">Articulos</button>
    |
    <button @click="funcMostrarComprobantes()">Comprobantes</button>
    <INFOrubros v-if="verINFOrubros"/>
    <INFOarticulos v-if="verINFOarticulos"/>
    <INFOcomprobantes v-if="verINFOcomprobantes"/>
  </div>
</template>

<script>
// @ is an alias to /src
import INFOrubros from '@/components/INFOrubros.vue'
import INFOarticulos from '@/components/INFOarticulos.vue'
import INFOcomprobantes from '@/components/INFOcomprobantes.vue'

export default {
  name: 'Home',
  components: {
    INFOrubros,
    INFOarticulos,
    INFOcomprobantes
  },
  data() {
    return {
        verINFOrubros: false,
        verINFOarticulos: false,
        verINFOcomprobantes: false
    }
  },
  methods: {
    funcMostrarRubros() {
      this.verINFOrubros = !this.verINFOrubros
    },
    funcMostrarArticulos() {
      this.verINFOarticulos = !this.verINFOarticulos
    },
    funcMostrarComprobantes() {
      this.verINFOcomprobantes = !this.verINFOcomprobantes
    },
  }
}
</script>
