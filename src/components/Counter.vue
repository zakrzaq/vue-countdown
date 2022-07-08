<template>
  <div>
    <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
    </section>
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
import { propsToAttrMap } from '@vue/shared'
import { computed, defineComponent, ref, ComputedRef, onMounted } from 'vue'
export default defineComponent({
  props: {
    date: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const displayDays = ref<string | number>(0)
    const displayHours = ref<string | number>(0)
    const displayMinutes = ref<string | number>(0)
    const displaySeconds = ref<string | number>(0)

    const _seconds: ComputedRef<number> = computed((): number => 1000)
    const _minutes: ComputedRef<number> = computed((): number => _seconds.value * 60)
    const _hours: ComputedRef<number> = computed((): number => _minutes.value * 60)
    const _days: ComputedRef<number> = computed((): number => _hours.value * 24)
    const theEnd: ComputedRef<string> = computed(() => props.date === '' ? dummyDate() : props.date)

    const formatCount = (count: number): number | string => {
      return count < 10 ? '0' + count : count
    }

    const dummyDate = () => {
      const d = new Date();
      const year = d.getFullYear();
      const month = d.getMonth();
      const day = d.getDate();
      const hour = d.getHours();
      const minute = d.getMinutes()
      const output = new Date(year + 1, month, day, hour, minute, 10, 10).toJSON();
      console.log(output.slice(0, -8))
      return output.slice(0, -8)
    }

    console.log(dummyDate())

    const showRemaining = () => {
      const timer = setInterval(() => {
        const now = new Date()
        const end = new Date(theEnd.value)

        const distance = end.getTime() - now.getTime()

        if (distance < 0) {
          clearInterval(timer)
          return
        }

        const seconds = Math.floor((distance % _minutes.value) / _seconds.value)
        const minutes = Math.floor((distance % _hours.value) / _minutes.value)
        const hours = Math.floor((distance % _days.value) / _hours.value)
        const days = Math.floor(distance / _days.value)

        displaySeconds.value = formatCount(seconds)
        displayMinutes.value = formatCount(minutes)
        displayHours.value = formatCount(hours)
        displayDays.value = formatCount(days)
      }, 1000)
    }

    onMounted(() => {
      showRemaining()
    })


    return {
      displayDays,
      displayHours,
      displayMinutes,
      displaySeconds,
    }
  }
})
</script>

<styles scoped>

</styles>


