<template>
  <div class="contact">
    <h1>Contact</h1>
    <TransitionGroup 
      tag="ul" 
      name="staggered"
      appear 
      @before-enter="beforeEnter"
      @enter="enter">
      <li v-for="(icon, idx) in icons" :key="icon.name" :data-index="idx">
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
import { ref } from 'vue'
import gsap from 'gsap'
export default {
  setup() {
    const icons = ref([
      { name: 'alternate_email', text: 'by email'},
      { name: 'local_phone', text: 'by phone'},
      { name: 'local_post_office', text: 'by post'},
      { name: 'local_fire_department', text: 'by smoke signal'},
    ])

    const beforeEnter = (el) => {
      el.style.opacity = 0;
      el.style.transform = 'translateY(400px)' // 400px from the bottom and not visible

    }
    
    const enter = (el, done) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 0.8,
        onComplete: done,
        delay: el.dataset.index * 0.2
      })
    }

    return { icons, enter, beforeEnter }
  }
}
</script>

<style>
  .contact ul {
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    max-width: 400px;
    margin: 60px auto;
  }
  .contact li {
    list-style-type: none;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    cursor: pointer;
    line-height: 1.5em;
  }
</style>