<template>
  <div class="ui segment">
    <div class="field" :class="completedClass" v-show="!isEditing">
        <input type="checkbox" @click="completeTodo" :checked="todo.done">
        <label @dblclick="showForm">{{ todo.title }}</label>
        <span class='times icon' @click="deleteTodo"><i class='times icon'></i></span>
    </div>
    <div v-show="isEditing" class="edit">
        <input type="text" 
               v-model="todo.title"
               :ref="name"
               @blur="hideForm"
               @keyup.enter="hideForm">
    </div>
  </div>
</template>

<script>
    export default{
        props: ['todo', 'id'],
        data(){
            return {
                isEditing: false,
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
                this.isEditing = true
                this.$nextTick(() => {
                    this.$refs[this.name].focus()
                })
            },
            hideForm(){
                this.isEditing = false
                this.$emit('edit-todo', {
                        title: this.todo.title,
                        done: this.todo.done
                    })
            },
            deleteTodo(){
                this.$emit('delete-todo')
            },
            completeTodo(){
                this.$emit('complete-todo')
            }
        }
    }
</script>

<style scoped>
    .ui.segment{padding:0;}
    .ui.segment span.times{
        display:none;
        position:absolute;
        right:10px;
        top:0;
        bottom:0;
        width:40px;
        height:40px;
        martgin:auto 0;
        font-size:20px;line-height:40px;
        color:#cc9a9a;
        margin-bottom: 11px;
        transition: color 0.2s ease-out;
    }
    .ui.segment:hover span.times{display:block;}

    .ui.segment .field label{display:block;white-space: pre-line;word-break:break-all;padding:1em 2em 1em 1em;margin-left: 45px;line-height: 1.2em;transition: color 0.4s;}
    .ui.segment .field.completed label{color:#d9d9d9;text-decoration: line-through;}

    .ui.segment .field input[type="checkbox"]{
        cursor: pointer;
        position: absolute;
        top: 1em;
        left: 1em;
        opacity: 0 !important;
        outline: 0;
        z-index: 3;
        width: 17px;
        height: 17px;
    }

    .ui.segment .field label:before{
        position:absolute;
        top: 1em;left:1em;
        width:17px;height:17px;
        content: '';
        background:#fff;
        border-radius:.21428571rem;
        -webkit-transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, -webkit-transform .1s ease, -webkit-box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, transform .1s ease, box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, transform .1s ease, box-shadow .1s ease, -webkit-transform .1s ease, -webkit-box-shadow .1s ease;
        border: 1px solid #d4d4d5;
    }
    .ui.segment .field input[type="checkbox"]:hover + label:before{border-color:#96c8da;}
    .ui.segment .field label:after {
        position: absolute;
        font-family: Checkbox;
        font-size: 14px;
        top: 1em;
        left: 1em;
        width: 17px;
        height: 17px;
        text-align: center;
        opacity: 0;
        color: rgba(0,0,0,.87);
        -webkit-transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,transform .1s ease,box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,transform .1s ease,box-shadow .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
    }
    .ui.segment .field input:checked ~ label:after {
        content: '\e800';
        opacity: 1;
        color: rgba(0,0,0,.95);
    }
    .edit{padding-left:45px;}
    .edit input[type="text"] {
        position: relative;
        margin: 0;
        width: 100%;
        font-family: inherit;
        font-weight: inherit;
        line-height: 1em;
        border: 0;
        outline: none;
        color: inherit;
        padding: 1em 1em;
        margin:0;
        border: 1px solid #999;
        box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
        -webkit-font-smoothing: antialiased;
        -moz-font-smoothing: antialiased;
        font-smoothing: antialiased;
    }
</style>