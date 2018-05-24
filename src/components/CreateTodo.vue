<template>
	<input placeholder="What needs to be done?"
		   class="new-todo" type="text"
  		   v-model="titleText"
  		   @keyup.enter="sendForm"
  		   autofocus
  		   autocomplete="off">
</template>

<script>
	export default{
		data(){
			return {
				titleText: ''
			}
		},
		methods: {
			sendForm(){
				if (this.titleText.length > 0) {
					this.$emit('create-todo', {
						title: this.titleText,
						done: false
					})
					this.titleText = ''
				}
			}
		}
	}
</script>

<style>

</style>