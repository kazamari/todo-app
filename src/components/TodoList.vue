<template>
	<div class="ui piled segments">
		<div class="ui segment header">
            <input v-if="todos.length" name="" type="checkbox" @click="completeAll" :checked="isCompleteAll">
            <label><create-todo @create-todo="addTodo"></create-todo></label>
        	
        </div>

		<todo v-for="(todo, index) in shownList"
				  :key="index"
				  :id = "index"
				  :todo="todo"
				  @delete-todo="deleteTodo"
				  @complete-todo="completeTodo(index)"
				  @edit-todo="editTodo($event, index)"></todo>
		<div class="ui secondary segment" v-if="todos.length">
			<div class="ui grid">
				<div class="four wide column">
					<p>Active Tasks: {{active.length}}</p>
				</div>
				<div class="eight wide column">
					<div class="ui basic buttons">
						<button class="ui button" :class="addClass('all')" @click="showList('all')">All</button>
						<button class="ui button" :class="addClass('active')" @click="showList('active')">Active</button>
						<button class="ui button" :class="addClass('completed')" @click="showList('completed')">Completed</button>
					</div>
				</div>
				<div class="four wide column">
					<button v-if="completed.length" class="ui basic button" @click="clearCompleted">Clear completed</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import Todo from './Todo'
	import CreateTodo from './CreateTodo'

	const filters = {
		all(todos){
			return todos
		},
		active(todos){
			return todos.filter((todo) => {
				return !todo.done
			})
		},
		completed(todos){
			return todos.filter((todo) => {
				return todo.done
			})
		}
	}
	
	export default{
		data() {
			return {
				todos: [],
				shown: 'all'
			}
		},
		watch: {
			todos() {
				this.writeToStorage()
			}
		},
		created(){
			if(localStorage.getItem('todos') === null){
				localStorage.setItem('todos', JSON.stringify([{
					title: 'Add task to list',
					done: false
				}]))
			}
			this.todos = JSON.parse(localStorage.getItem('todos'))
		},
		computed: {
			shownList(){
				return filters[this.shown](this.todos)
			},
			completed(){
				return filters.completed(this.todos)
			},
			active(){
				return filters.active(this.todos)
			},
			isCompleteAll(){
				return this.todos.length === this.completed.length && this.todos.length > 0
			}
		},
		methods: {
			addClass(shown){
				if (this.shown === shown){
					return 'active'
				}
			},
			showList(shown){
				this.shown = shown
			},
			editTodo(event, index){
				this.todos[index] = event
			},
			deleteTodo(event, i){
				let index = this.todos.indexOf(event)
				this.todos.splice(index, 1)
			},
			completeAll(e){
				for(let todo of this.todos){
					todo.done = e.target.checked ? true : false
				}
				this.showList('all')
			},
			addTodo(event){
				this.todos.push(event)
			},
			clearCompleted(){
				this.todos = this.active
			},
			writeToStorage(){
				localStorage.setItem('todos', JSON.stringify(this.todos))
			}
		},
		components: {
			Todo,
			CreateTodo
		}
	}
</script>

<style>

</style>