<template>
	<ul class="todo-main" v-show="todoList.length">
		<MyItem 
			v-for="todo in todoList" 
			:key="todo.id" 
			:todo="todo"
			:deleteTodo="deleteTodo"
			:checkedTodo="checkedTodo"
		/>
	</ul>
</template>

<script>
	import MyItem from './MyItem'

	export default {
		name:'MyList',
		components:{MyItem},
		props:['todoList', 'deleteTodo', 'checkedTodo']
	}
</script>

<style scoped>
	/*main*/
	.todo-main {
		margin-left: 0px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding: 0px;
	}

	.todo-empty {
		height: 40px;
		line-height: 40px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding-left: 5px;
		margin-top: 10px;
	}
</style>