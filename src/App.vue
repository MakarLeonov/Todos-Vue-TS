<template>
  <div>
    
    <AppHeader />

    <AppFilters :ative-filter="activeFilter" @set-filter="(filter: Filter) => activeFilter = filter"/>

    <main class="app-main">
      <AppToDoList :todos="filteredTodos" @toggle-todo="toggleTodo" @remove-todo="removeTodo"/>  
      <AppAddToDo @add-todo="addTodo"/>
    </main>
    
    <AppFooter :amoutn="todos.length" :done="done"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppHeader from './components/AppHeader.vue';
import AppFilters from './components/AppFilters.vue';
import AppToDoList from './components/AppToDoList.vue';
import AppAddToDo from './components/AppAddToDo.vue';
import AppFooter from './components/AppFooter.vue';
import { Todo } from './types/Todo';
import { Filter } from './types/Filter';

interface State {
  todos: Todo[],
  activeFilter: Filter,
}

export default defineComponent({
  components: { 
    AppHeader,
    AppFilters,
    AppToDoList,
    AppAddToDo,
    AppFooter,
  },

  data(): State {
    return {
      todos: [
        {id: 0, text: 'Learn TypeScript', complited: false},
        {id: 1, text: 'Create the app', complited: true},
        {id: 2, text: 'memes are insain!!!', complited: false},
      ],
      activeFilter: 'All'
    }
  },

  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'All':
          return this.todos
        case 'Active':
          return this.todos.filter((todo: Todo) => !todo.complited)
        case 'Done':
          return this.todos.filter((todo: Todo) => todo.complited)
      }
    },

    done(): number {
      return this.todos.filter((el: Todo) => el.complited).length
    }
  },

  methods: {
    addTodo(todo: Todo){
      this.todos.push(todo)
    },

    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)

      if (targetTodo) {
        targetTodo.complited = !targetTodo.complited
      }
    },

    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    }
  }
})
</script>
