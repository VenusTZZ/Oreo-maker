<script setup lang="ts">
import Button from "./components/Button.vue"
import Canvas from './components/Canvas.vue'
const handleClick = () => {
  console.log("handle")
  show = true
}

const oreoList = $ref<string[]>([])
let show = $ref(false)

const addSlice = (key: 'o' | 'r' | '-' | '-1') => {
  switch (key) {
    case 'o':
      const addKey = oreoList.values.length === 0 ? 'o' : 'ob'
      oreoList.push(addKey)
      break;
    case 'r':
      oreoList.push('r')
      break;
    case '-':
      if (oreoList.length > 1 && oreoList[oreoList.length - 1] !== '-') {
        oreoList.push('-')
      }
      break;
    case '-1':
      oreoList.pop()
  }
}
</script>

<template>
  <div flex items-center box-border h-screen w-screen bg="#a4e2c6" p-12>
    <main bg-white flex="~ col" w-full p-8 rounded-xl shadow="md black/20">
      <header>
        <h1 text="center 2xl" font-bold>
          title
        </h1>
      </header>
      <main py-4>
        <div flex="~" items-center justify-center text-xl text-truegray-300 min-h-12 bg-gray-100 rounded-xl
          border="~ truegray-200">
          我的Oreo
        </div>
        <div py-2>
          {{oreoList}}
        </div>
        <div flex py-4 h-10 items-center justify-center gap-4>
          <Button @click="addSlice('o')">要奥</Button>
          <Button @click="addSlice('r')">要利</Button>
          <Button @click="addSlice('-')">在来</Button>
          <Button @click="addSlice('-1')">不要</Button>
        </div>
      </main>
      <main v-if="show" h="400px">
        <Canvas :input="oreoList" />
      </main>
      <footer flex items-center justify-center mx="-8" mb="-8" h-16 text="white xl" cursor-pointer bg-truegray-700
        hover="bg-gray-800 text-2xl" text-white rounded-b-xl @click="handleClick">
        快给我
      </footer>
    </main>
  </div>


</template>
<style>
html,
body {
  margin: 0;
  padding: 0;
}
</style>