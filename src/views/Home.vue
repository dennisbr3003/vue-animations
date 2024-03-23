<template>
  <div class="home">
    <Toast v-if="showToast" />
    <Todos @badValue="triggerToast" />
    <Transition name="diok">
      <div v-if="showdiv">
        <h1>Hello Dennis</h1>
      </div>
    </Transition>
    <button @click="showdiv=!showdiv" style="margin-top: 15px; padding: 5px 8px;">toggle</button>
  </div>
</template>

<script>
import { ref } from 'vue'
import Toast from '../components/Toast'
import Todos from '../components/Todos'

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false)
    const showdiv = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }

    return { showToast, showdiv, triggerToast }
  }
}
</script>

<style scoped>

.diok-enter-from {
  opacity: 0;
}
.diok-enter-to {  /* this class can be omitted because it is the default state of the element (unless you want to deviate) */
  opacity: 1;
}
.diok-enter-active {
  transition: all 2s ease;
}

.diok-leave-from {  /* this class can be omitted because it is the default state of the element (unless you want to deviate) */
  opacity: 1;
}
.diok-leave-to {
  opacity: 0;
}
.diok-leave-active {
  transition: opacity 2s ease;
}

</style>