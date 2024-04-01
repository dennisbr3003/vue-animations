<template>
  <div class="about">
    <Transition 
      name="fade" 
      appear
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave"
      >
      <h1 v-if="showTitle">About</h1>
    </Transition>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {

    const showTitle=ref(true)

    const beforeEnter = (el) => {
      console.log('before enter', el)
    }
    const enter = (el) => {
      console.log('enter', el)
    }
    const afterEnter = (el) => {
      console.log('after enter - run timeout function', el)
      el.style.color='red'
      setTimeout(()=> showTitle.value=false, 3000)
    }
    const beforeLeave = (el) => {
      el.style.color='pink'
      console.log('before leave', el)
    }
    const leave = (el) => {
      console.log('leave', el)
    }
    const afterLeave = (el) => {
      console.log('after leave', el)
    }    
    return { showTitle, beforeEnter, enter, afterEnter, beforeLeave, leave, afterLeave }
  }
}
</script>

<style>
  .about {
    max-width: 600px;
    margin: 20px auto;
  }

  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 3s ease;
  }
  .fade-leave-to {
    opacity: 0; 
  }
  .fade-leave-active {
    transition: opacity 3s ease;
  }
</style>