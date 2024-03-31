<template>
  <div class="todos">
    <input 
      type="text" 
      v-model="newTodo" 
      @keypress.enter="addTodo"
      placeholder="Add a new todo..."
    />
    <Transition name="todolist" mode="out-in">
      <div v-if="todos.length">
        <!-- <ul> -->        
        <TransitionGroup tag="ul" name="list" appear>  <!-- appear prop is applying transition on page load it will use the enter classes -->
          <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
            {{ todo.text }}
          </li>
        </TransitionGroup>
        <!-- </ul> -->
      </div>
      <div v-else>Woohoo, nothing left todo!</div>
    </Transition>  
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup(props, { emit }) {
    const todos = ref([
      { text: 'Make the bed', id: 1 },
      { text: 'Play video games', id: 2 },
      { text: 'Do something useful', id: 3 },
      { text: 'Do something useful 2', id: 4 },
    ])
    const newTodo = ref('')

    const addTodo = () => {
      if (newTodo.value) {
        const id = Math.random()
        todos.value = [{ text: newTodo.value, id }, ...todos.value]
        newTodo.value = ''
      } else {
        emit('badValue')
      }
    }

    const deleteTodo = (id) => {
      todos.value = todos.value.filter(todo => todo.id != id)
    }

    return { todos, addTodo, deleteTodo, newTodo }
  }
}
</script>

<style>
  .todos {
    max-width: 400px;
    margin: 20px auto;
    position: relative;
  }
  input {
    width: 100%;
    padding: 12px;
    border: 1px solid #eee;
    border-radius: 10px;
    box-sizing: border-box;
    margin-bottom: 20px;
  }
  .todos ul {
    position: relative; /* essential for the move animation (class=list-leave-active) */
    padding: 0;
  }
  .todos li {
    list-style-type: none;
    display: block;
    margin-bottom: 10px;
    padding: 10px;
    background: white;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    border-radius: 10px;
    width: 100%;
    box-sizing: border-box;
  }
  .todos li:hover {
    cursor: pointer;
  }

/* list transition classes */

.list-enter-from {
  opacity: 0;
  transform: scale(0.6, 0.1); /* the element(s) start at 60% of it's original size (width) and 10% of it's original height */
}
.list-enter-to {
  opacity: 1;
  transform: scale(1);
}
.list-enter-active {
  transition: all 0.4s ease;
}

.list-leave-from {
  opacity: 1;
  transform: scale(1); /* the element(s) start at 60% of it's original size */
}
.list-leave-to {
  opacity: 0;
  transform: scale(0.6, 0.1);
}
.list-leave-active {
  transition: all 0.4s ease;
  position: absolute; /* <-- add this if you want the move class to also work when removing an item make sure the surrounding UL class is positioned relative */
}
/* this applies to transition groups only when a item is added it slides in */
.list-move {
  transition: all 0.3s ease;
}

/* switch transitions */

.todolist-enter-from, .todolist-leave-to {
  opacity: 0;
  transform: translateY(20px)
}
/* this one could go */
.todolist-enter-to, .todolist-leave-from {
  opacity: 1;
  transform: translateY(0)
}
.todolist-enter-active, .todolist-leave-active {
  transition: all 0.5s ease;
}
</style>