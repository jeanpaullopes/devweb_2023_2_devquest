<template>


  <q-card class="fasecard"
    :style="getBackground()">
    <q-card-section>
      {{ fase }}
      <q-btn label="Open Dialog" @click="open = true" />
      <h5>{{ objFase.titulo }}</h5>
      {{ objFase.texto }}
    </q-card-section>
    <q-card-actions style="background-color: aqua;">

      <q-btn v-for="op in objFase.opcoes" v-bind:key="op"
       :label="op.texto" @click="gritar(op.destino)"/>
    </q-card-actions>
  </q-card>

  <q-dialog v-model="open">
      <q-layout view="Lhh lpR fff" container class="bg-white text-dark">
        <q-header class="bg-primary">
          <q-toolbar>
            <q-btn flat @click="drawer = !drawer" round dense icon="menu" />
            <q-toolbar-title>Header</q-toolbar-title>
            <q-btn flat @click="drawerR = !drawerR" round dense icon="menu" />
            <q-btn flat v-close-popup round dense icon="close" />
          </q-toolbar>
        </q-header>

        <q-footer class="bg-black text-white">
          <q-toolbar>
            <q-toolbar-title>Footer</q-toolbar-title>
          </q-toolbar>
        </q-footer>

        <q-drawer bordered v-model="drawer" :width="200" :breakpoint="600" class="bg-grey-3 text-dark q-pa-sm">
          <div v-for="n in 50" :key="n">Drawer {{ n }} / 50</div>
        </q-drawer>

        <q-drawer side="right" bordered v-model="drawerR" :width="200" :breakpoint="300" class="bg-grey-3 text-dark q-pa-sm">
          <div v-for="n in 50" :key="n">Drawer {{ n }} / 50</div>
        </q-drawer>

        <q-page-container>
          <q-page padding>
              {{ objFase.texto}}

          </q-page>
        </q-page-container>
      </q-layout>
    </q-dialog>


</template>

<script>
import axios from 'src/boot/axios';
export default {
  name: 'FaseCard',
  emits: ['gritei'],

  props: {
    fase: {
      type: Object,
      required: false
    }
  },
  watch: {
    fase(val, oldVal) {
      this.carregaFase(val)
    }
  },
  data() {
    return {
      open: false,
      objFase: Object
    }
  },
  methods: {
    gritar(val) {
      this.$emit('gritei', val)
    },
    getBackground() {
      return 'background-size: cover; background-image: url('+this.objFase.background+')'
    },
    carregaFase(i) {
      const axios = require('axios');
    const consulta = axios.get('http://localhost:3000/fases/'+
                                i)
    .then((response)=>{
      this.objFase = response.data
      console.log(response.data)
    })
    .catch((error)=>{
      console.log(error)
    })
    }
  },
  computed: {
  },
  created() {
    this.carregaFase(this.fase)
  },
}
</script>

<style>
  .fasecard {
      width: 90vw;
    }
</style>
