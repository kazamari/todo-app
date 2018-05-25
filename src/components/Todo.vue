<template>
  <div class="ui segment">
    <div class="field" :class="completedClass" v-show="!editedTodo">
        <input type="checkbox" v-model="todo.done">
        <label @dblclick="showForm(todo)">{{ todo.title }}</label>
        <span class='times icon' @click="deleteTodo"><i class='times icon'></i></span>
    </div>
    <div v-show="editedTodo" class="edit">
        <input type="text" 
               v-model="todo.title"
               :ref="name"
               @blur="hideForm"
               @keyup.enter="hideForm"
               @keyup.esc="cancelEdit">
    </div>
  </div>
</template>

<script>
    export default{
        props: ['todo', 'id'],
        data(){
            return {
                editedTodo: null,
                name: 'td_' + this.id
            }
        },
        computed:{
            completedClass(){
                return this.todo.done ? "completed" : ""
            }
        },
        methods: {
            showForm(){
                this.beforeEditCache = this.todo.title;
                this.editedTodo = this.todo;
                this.$nextTick(() => {
                    this.$refs[this.name].focus()
                })
            },
            hideForm(){
                this.editedTodo = null
                this.todo.title = this.todo.title.trim()
                if (!this.todo.title) {
                    this.$emit('delete-todo', this.todo)
                } else {
                    this.$emit('edit-todo', this.todo)
                }
                /*this.$emit('edit-todo', {
                        title: this.todo.title.trim(),
                        done: this.todo.done
                    })*/
            },
            cancelEdit(){
                this.editedTodo = null
                this.todo.title = this.beforeEditCache
            },
            deleteTodo(){
                this.$emit('delete-todo', this.todo)
            }
        }
    }
</script>

<style>

</style>