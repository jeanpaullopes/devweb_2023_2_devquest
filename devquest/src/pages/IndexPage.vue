<template>
  <q-page class="flex flex-center">
    <FaseCard fase="1"/>

  </q-page>
</template>

<script>
import FaseCard from 'src/components/FaseCard.vue';
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'IndexPage',
    components: { FaseCard }
})
</script>
