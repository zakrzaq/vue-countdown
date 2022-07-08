<template>
  <input type="datetime-local" v-model="selectedDate" />
  <Counter :date="selectedDate" />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import Counter from '../components/Counter.vue'

export default defineComponent({
  name: 'HomeView',
  components: {
    Counter
  },
  setup() {
    const selectedDate = ref('')

    return {
      selectedDate,
    }
  },
})
</script>

<style scoped>
</style>
