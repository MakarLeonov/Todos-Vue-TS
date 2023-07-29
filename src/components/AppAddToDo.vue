<template>
    <section class="add-todo">
        <form 
          class="add-todo__form" 
          v-if="isFormVisible"
          @submit.prevent="addTodo"
          >
          <button class="close-button" type="button" @click="formToggle">
            <i class="bi bi-x"></i>
          </button>
          <div class="text-input text-input--focus">
            <input class="input" v-model="formText" @keyup.ctrl.enter="addTodo"/>
          </div>
          <button class="button button--filled" >Add task</button>
        </form>

        <button class="add-todo__show-form-button" v-else @click="formToggle">
          <i class="bi bi-plus-lg"></i>
        </button>
      </section>
</template>

<script lang="ts">
import { Todo } from '@/types/Todo'
import { defineComponent } from 'vue'

interface State{
  isFormVisible: boolean,
  formText: string,
}

export default defineComponent({
  data() {
    return {
      isFormVisible: false,
      formText: ''
    }
  },

  methods: {
    formToggle() {
      this.isFormVisible = !this.isFormVisible
    },

    addTodo() {
      if (this.formText) {
        this.$emit('addTodo', {
          id: Date.now(),
          text: this.formText,
          complited: false,
        }),
        this.formText = ''
      }
    }
  },

  emits: {
    addTodo: (todo: Todo) => todo
  }

  
})
</script>