<template>
	<div class="ui piled segments">
		<div class="ui segment header">
            <input name="" type="checkbox" @click="completeAll" :checked="isCompleteAll">
            <label><create-todo @create-todo="addTodo"></create-todo></label>
        	
        </div>
		<todo v-for="(todo, index) in shownList"
				  :key="index"
				  :id = "index"
				  :todo="todo"
				  @delete-todo="deleteTodo(index)"
				  @complete-todo="completeTodo(index)"
				  @edit-todo="editTodo($event, index)"></todo>
		<div class="ui secondary segment">
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
					<button class="ui basic button" @click="clearCompleted">Clear completed</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import Todo from './Todo'
	import CreateTodo from './CreateTodo'
	
	export default{
		data() {
			return {
				todos: [],
				shown: 'all'
			}
		},
		mounted(){
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
				if (this.shown === 'active'){
					return this.active
				}else if (this.shown === 'completed'){
					return this.completed
				}else{
					return this.todos
				}
			},
			completed(){
				return this.todos.filter(todo => {return todo.done === true})
			},
			active(){
				return this.todos.filter(todo => {return todo.done === false})
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
				this.writeToStorage()
			},
			deleteTodo(index){
				this.todos.splice(index, 1)
				this.writeToStorage()
			},
			completeTodo(index){
				this.todos[index].done = !this.todos[index].done
				this.writeToStorage()
			},
			completeAll(e){
				for(let todo of this.todos){
					todo.done = e.target.checked ? true : false
				}
				this.showList('all')
				this.writeToStorage()
			},
			addTodo(event){
				this.todos.push(event)
				this.showList('all')
				this.writeToStorage()
			},
			clearCompleted(){
				this.todos = this.active
				this.showList('all')
				this.writeToStorage()
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