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

    <div style="display: flex; flex-direction: row; align-items: center; gap: 20px; width: fit-content; margin: auto; margin-top: 50px; transform: scale(0.5);">
      <Transition 
        name="circle" 
        appear
        @before-enter="beforeEnter"
        @enter="enter"
        @after-enter="afterEnter"
        >
        <div class="full-circle">
          <Transition name="line1" appear> 
            <div class="diagonal-line"/>
          </Transition>    
          <Transition name="line2" appear>
            <div class="diagonal-line2"/>
          </Transition>  
        </div>      
      </Transition>
      <div>
        <Transition
          name="text"
          appear
          @before-enter="beforeEnter1"
          @enter="enter1"
          @after-enter="afterEnter1"
        >  
          <div class="text" id="test">Some error occured</div>
        </Transition>
        <transition
          name="underline"
          appear
          @before-enter="beforeEnter2"
          @enter="enter2"
          @after-enter="afterEnter2"

        >
          <div style="border-bottom: 10px solid red;"></div>
        </transition>
      </div>
    </div>    
  </div>
</template>

<script>
import { ref } from 'vue'
import Toast from '../components/Toast'
import Todos from '../components/Todos'
import gsap from 'gsap'

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false)
    const showdiv = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }
    const beforeEnter = (el) => {
      el.style.transform = 'translateY(-600px)' // move out of the window (to the top)
      el.style.opacity = 0
    }

    const enter = (el, done) => {
      gsap.to(el, {
        y: 0, // translate Y to 0 = original position
        opacity: 1,
        duration: 2, // seconds
        ease: 'bounce.out',
        onComplete: done // needed to tell vue the animation is done or it will fire afterEnter to soon
      })
    }

    const afterEnter = (el) => {
    }

    const beforeEnter1 = (el) => {
      el.style.transform = 'scale(1, 0)'
    }
    const enter1 = (el, done) => {
      gsap.to(el, {
        duration: 1, // seconds
        scaleX: 1,
        scaleY: 1,
        ease: 'ease',
        delay: 1,
        onComplete: done // needed to tell vue the animation is done or it will fire afterEnter to soon
      })      
      
    }
    const afterEnter1 = (el) => {
      gsap.to(el, {
        keyframes: {
          "20%": {skewY: 8},
          "40%": {skewY: -8},
          "60%": {skewY: 4},
          "80%": {skewY: -4},
          "100%": {skewY: 0}
        },
        duration: 0.3, // seconds
      })            
    }
    
    const beforeEnter2 = (el) => {
      el.style.transform = 'scaleX(0)'
      el.style.opacity = 0
    }

    const enter2 = (el, done) => {
      gsap.to(el, {
        duration: 2.3, // seconds
        scaleX: 1,
        opacity: 1,
        ease: 'ease-out',
        onComplete: done // needed to tell vue the animation is done or it will fire afterEnter to soon
      })      
      
    }
    const afterEnter2 = (el) => {
    }

    return { showToast, showdiv, triggerToast, enter, afterEnter, beforeEnter, enter1, afterEnter1, beforeEnter1, enter2, afterEnter2, beforeEnter2}
  }
}
</script>

<style scoped>
/*

.cube {
  width:40px;
  height:40px;
  background:#000;
  
  animation:spin 3s;
  animation-iteration-count:infinite;
}
@keyframes spin {
  from {
    transform:rotate(0deg);
  }
  to {
    transform:rotate(360deg);
  }
}
*/
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
.text {
  color: red;
  font-size: 48pt;
  font-weight: 500;
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

/* lines */

.line1-enter-from {
  width: 0px;
  transform: rotate(0deg);
}
.line1-enter-to {
  width: 90px;
  transform: rotate(45deg);
}
.line1-enter-active {
  animation: grow1 1.5s ease;
}
.line2-enter-from {
  width: 0px;
}
.line2-enter-to {
  width: 90px;
}
.line2-enter-active {
  animation: grow2 1.5s ease;
}

.full-circle{
  display: block;
  border: 10px solid red;  
  border-radius: 50%;
  width: 100px;
  height: 100px;
  position: relative;
}

.diagonal-line{
  position: absolute;
  border-radius: 5px;
  border-top: 10px solid red;
  width: 90px; 
  height: 0px;
  transform: rotate(45deg);
  top: 45px;
  left: 5px;
}
.diagonal-line2{
  position: absolute;
  border-radius: 5px;
  border-top: 10px solid red;
  width: 90px;
  height: 0px;
  transform: rotate(135deg);
  top: 45px; /* 100px - 10px / 2 */
  left: 5px;  
}

@keyframes grow1 {
  0% {
    width: 0px;
    left: 50px;
    transform: rotate(0deg);
  }
  10% {
    width: 10px;
    left: 45px;
    transform: rotate(5deg);
  }
  20% {
    width: 20px;
    left: 40px;
    transform: rotate(10deg);
    }
  30% {
    width: 30px;
    left: 35px;
    transform: rotate(15deg);
  }
  40% {
    width: 40px;
    left: 30px;
    transform: rotate(20deg);
  }
  50% {
    width: 50px;
    left: 25px;
    transform: rotate(25deg);
  }
  60% {
    width: 60px;
    left: 20px; 
    transform: rotate(30deg); 
  }  
  70% {
    width: 70px;
    left: 15px;  
    transform: rotate(35deg);
  }
  80% {
    width: 80px;
    left: 10px;  
    transform: rotate(40deg);
  }      
  90% {
    width: 90px;
    left: 5px;  
    transform: rotate(45deg);
  }  
  100%{    
    width: 90px;
    left: 5px;  
    transform: rotate(45deg);
  }
}
@keyframes grow2 {
  0% {
    width: 0px;
    left: 50px;
    transform: rotate(0deg);
  }
  10% {
    width: 10px;
    left: 45px;
    transform: rotate(13.5deg);
  }
  20% {
    width: 20px;
    left: 40px;
    transform: rotate(40.5deg);
    }
  30% {
    width: 30px;
    left: 35px;
    transform: rotate(50.4deg);
  }
  40% {
    width: 40px;
    left: 30px;
    transform: rotate(67.5deg);
  }
  50% {
    width: 50px;
    left: 25px;
    transform: rotate(81deg);
  }
  60% {
    width: 60px;
    left: 20px; 
    transform: rotate(94.5deg); 
  }  
  70% {
    width: 70px;
    left: 15px;  
    transform: rotate(108deg);
  }
  80% {
    width: 80px;
    left: 10px;  
    transform: rotate(121.5deg);
  }      
  90% {
    width: 90px;
    left: 5px;  
    transform: rotate(135deg);
  }  
  100%{    
    width: 90px;
    left: 5px;  
    transform: rotate(135deg);
  }
}
@keyframes wobble2 {
  20% {
    transform:skewY(8deg)
  }
  40% {
    transform:skewY(-8deg)
  }
  60% {
    transform:skewY(4deg)
  }
  80% {
    transform:skewY(-4deg)
  }
}
</style>