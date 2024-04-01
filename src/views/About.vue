<template>
  <div class="about">
    <!--  ep-10
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave"
    -->
    <Transition 
      name="fade" 
      appear
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      >
      <!-- ep-10 <h1 v-if="showTitle">About</h1> -->
      <h1>About</h1>
    </Transition>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
  </div>
</template>

<script>
// import { ref } from 'vue'
import gsap from 'gsap'
export default {
  setup() {

    // const showTitle=ref(true)

    const beforeEnter = (el) => {
      console.log('before enter - set initial state')
      el.style.transform = 'translateY(-140px)' // move out of the window (to the top)
      el.style.opacity = 0
    }

    const enter = (el, done) => {
      console.log('starting to enter - making transition')      
      gsap.to(el, {
        y: 0, // translate Y to 0 = original position
        opacity: 1,
        duration: 2, // seconds
        ease: 'bounce.out',
        onComplete: done // needed to tell vue the animation is done or it will fire afterEnter to soon
      })
    }

    const afterEnter = (el) => {
      console.log('after enter')
    }

    // const beforeEnter = (el) => {
    //   console.log('before enter', el)
    // }
    // const enter = (el) => {
    //   console.log('enter', el)
    // }
    // const afterEnter = (el) => {
    //   el.style.color='red'
    //   setTimeout(()=> showTitle.value=false, 3000)
    // }
    // const beforeLeave = (el) => {
    //   console.log('before leave', el)
    // }
    // const leave = (el) => {
    //   el.style.animation="shrink 2s ease"      
    // }
    // const afterLeave = (el) => {
    //   showTitle.value=true
    // }    
    // return { showTitle, beforeEnter, enter, afterEnter, beforeLeave, leave, afterLeave }

    return { beforeEnter, enter, afterEnter}

  }
}
</script>

<style>
  .about {
    max-width: 600px;
    margin: 20px auto;
  }
/* (ep-10)
  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 3s ease;
  }
  @keyframes shrink {
    0% {
      opacity: 1;
      transform: scale(1, 1); 
    }
    10% {
      opacity: 0.90;
      transform: scale(1, 0.9); 
    }
    20% {
      opacity: 0.80;
      transform: scale(1, 0.8); 
    }    
    30% {
      opacity: 0.70;
      transform: scale(1, 0.7); 
    }    
    40% {
      opacity: 0.60;
      transform: scale(1, 0.6); 
    }    
    50% {
      opacity: 0.50;
      transform: scale(1, 0.5); 
    }    
    60% {
      opacity: 0.40;
      transform: scale(1, 0.4); 
    }    
    70% {
      opacity: 0.30;
      transform: scale(1, 0.3); 
    }    
    80% {
      opacity: 0.20;
      transform: scale(1, 0.2); 
    }    
    90% {
      opacity: 0.10;
      transform: scale(1, 0.1); 
    }    
    100% {
      opacity: 0;
      transform: scale(1, 0); 
    }    
  } */
</style>