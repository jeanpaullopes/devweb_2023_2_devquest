<template>
  {{ idx }}
  <q-page class="flex flex-center">
    <FaseCard :fase="idx" @gritei="trataEvento"/>
    <FaseCard :fase="idx+1" @gritei="trataEvento"/>

  </q-page>
</template>

<script>
import FaseCard from 'src/components/FaseCard.vue';
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'IndexPage',
    components: { FaseCard },
    data() {
        return {
          idx: 1
        }
    },
    methods: {
      trataEvento(val) {
        this.idx = val
      }
    }
})
</script>
