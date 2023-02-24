<script setup>
import { ref,reactive } from 'vue'

defineProps({
  msg: String,
})
const proxy = reactive({}) // 深层响应式

const raw = { a: 2}
proxy.nested = raw
console.log(proxy.nested === raw) // false

const count = ref(0)

function methodHandlerEvent(event,args){
  console.log(event.key)
  console.log(event.target,args)
}
function keyUpHandler(event) {
  console.log(event.key)
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <button type="button" @click="proxy.nested.a++">count is {{ proxy.nested.a }}</button>
    <button type="button" @click="methodHandlerEvent($event,2)">methodHandlerEvent</button>
    <!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
    <input  @keyup.enter="keyUpHandler($event)" />
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
