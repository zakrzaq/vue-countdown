<template>
  <div>
    <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">Counter</section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{ displayDays }}
        <div class="label text-sm absolute bottom-0">Days</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="hours mr-2 relative">
        {{ displayHours }}
        <div class="label text-sm absolute bottom-0">Hours</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="minutes mr-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute bottom-0">Minutes</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="secnds mr-2 relative">
        {{ displaySeconds }}
        <div class="label text-sm absolute bottom-0">Seconds</div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
export default defineComponent({
  setup() {
    const displayDays = ref(0)
    const displayHours = ref(0)
    const displayMinutes = ref(0)
    const displaySeconds = ref(0)



    return {
      displayDays,
      displayHours,
      displayMinutes,
      displaySeconds
    }
  }
})
</script>

<styles scoped>

</styles>


