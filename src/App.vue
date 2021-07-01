<!--
 * @Author: hhhhhq
 * @Date: 2021-07-02 07:44:56
 * @LastEditors: hhhhhq
 * @LastEditTime: 2021-07-02 07:58:05
 * @Description: file content
-->
<template>
  <div>
    <h1>Vue watchEffect demo</h1>
    <textarea v-model="textContent" />
    <p v-if="isTyping">Jld is typing ...</p>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue"

export default {
  setup() {
    const textContent = ref("")
    const isTyping = ref(false)

    const stop = watchEffect(onInvalidate => {
      if (textContent.value.length > 0) {
        isTyping.value = true

        if (textContent.value.length > 10) {
          stop()
        }

        const showTypingStatus = setTimeout(() => {
          isTyping.value = false
        }, 2000)

        onInvalidate(() => {
          clearInterval(showTypingStatus)
        })
      }
    })

    return {
      textContent,
      isTyping,
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
