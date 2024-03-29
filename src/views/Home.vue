<template>
  <div class="home">
    <!-- <Transition name="xtoast">
      <Toast v-if="showToast" />
    </Transition> -->
    <Transition name="xtoasta">
      <Toast v-if="showToast" />
    </Transition>    
    <Todos @badValue="triggerToast" />
    <Transition name="diok">
      <div v-if="showdiv">
        <h1>Hello Dennis</h1>
        <div>Test 123</div>
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

/* not used when using a animation */
/* enter classes */
.xtoast-enter-from {
  opacity: 0;
  transform: translateY(-60px); /* initially we set it off the screen with a transform and negative pixels */
}
.xtoast-enter-to {
  opacity: 1;
  transform: translateY(0);  /* make it appear at its original location from the top at the end of the transition */
}

.xtoast-enter-active {
  transition: all 0.5s ease;
}

.xtoasta-enter-active {
  animation: wobble 0.5s ease; /* animation is in keyframes */
}

/* leave classes */
.xtoasta-leave-from {
  opacity: 1;
  transform: translateY(0); /* initially we we acknowledge the original location */
}
.xtoasta-leave-to {
  opacity: 0;
  transform: translateY(-60px); /* make it end up 60 pixels off the screen at the end of the transition*/ 
}
.xtoasta-leave-active {
  transition: all 0.3s ease;
}

/* leave classes */
.xtoast-leave-from {
  opacity: 1;
  transform: translateY(0); /* initially we we acknowledge the original location */
}
.xtoast-leave-to {
  opacity: 0;
  transform: translateY(-60px); /* make it end up 60 pixels off the screen at the end of the transition*/ 
}
.xtoast-leave-active {
  transition: all 0.3s ease;
}

/* use this deatiled animation sequence in active class */
/* depending on where you use it, this replaces the from, to and active classes because it incorporates it */
@keyframes wobble {
  0% {
    opacity: 0;
    transform: translateY(-60px);
  }
  50% {
    transform: translateY(0);
    opacity: 1;
  }
  60% {
    /* transform: translateX(8px); */
    transform:skewY(8deg)
  }
  70% {
    /* transform: translateX(-8px); */
    transform:skewY(-8deg)
  }
  80% {
    /* transform: translateX(4px); */
    transform:skewY(4deg)
  }
  90% {
    /* transform: translateX(-4px); */
    transform:skewY(-4deg)
  }
  100% {
    transform: translateX(0);
  }  
}
</style>