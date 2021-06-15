<template>
  <div class="flex h-screen ">
    <div class="w-[200px] border-1 border-black flex-none">
      <input @focusout="check" v-model="integer" class="border-[1px] border-black" type="number">
    </div>
    <div class="w-48 border-l-2 border-r-2 border-black flex-1 min-w-[100px]">
      <select class="border-[1px] border-black" name="type" v-model="mode" @change="check">
        <option value="isPrime">isPrime</option>
        <option value="isFibonacci">isFibonacci</option>
      </select>
    </div>
    <div class="w-[300px] border-1 border-black flex-none">
      <div> {{ result }} </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {
    const integer = 1
    const mode = 'isPrime'
    const result: any = ''
    return { integer, mode, result }
  },
  methods: {
    calPrime(num: number) {
      let isPrime = true
      for (let i = 2; i < this.integer; i++) {
        if (this.integer % i === 0) isPrime = false
      }
      return isPrime
    },
    calFibo(num: number) {
      let left = 0
      let right = 1
      while (right < num) {
        const _right = right
        right += left
        left = _right
      }
      return right === num
    },
    check(e: Event) {
      if (this.integer <= 0) this.integer = 1
      this.integer = Math.round(this.integer)

      if (this.mode === 'isPrime') {
        this.result = this.calPrime(this.integer)
      } else {
        this.result = this.calFibo(this.integer)
      }
    }
  }
})
</script>


<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
