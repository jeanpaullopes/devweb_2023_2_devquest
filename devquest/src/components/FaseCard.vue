<template>
  <div >
    asdasd≤<br/>
    {{ objFase.background }}
    asdasd≤<br/>asdasd≤<br/>asdasd≤<br/>asdasd≤<br/>asdasd≤<br/>
</div>

  <q-card class="fasecard"
    :style="getBackground()">
    <q-card-section>
      <h5>{{ objFase.titulo }}</h5>
      {{ objFase.texto }}
    </q-card-section>
  </q-card>
</template>

<script>
import axios from 'src/boot/axios';
export default {
  name: 'FaseCard',
  props: {
    fase: {
      type: Object,
      required: false
    }
  },
  data() {
    return {
      objFase: Object
    }
  },
  methods: {
    getBackground() {
      return 'background: url('+this.objFase.background+')'
    }
  },
  computed: {
  },
  created() {
    const axios = require('axios');
    const consulta = axios.get('http://localhost:3000/fases/'+
                                this.fase)
    .then((response)=>{
      this.objFase = response.data
      console.log(response.data)
    })
    .catch((error)=>{
      console.log(error)
    })
  },
}
</script>

<style>
  .fasecard {
      width: 90vw;
    }
</style>
