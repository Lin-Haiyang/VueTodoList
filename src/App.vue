<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader :addTodo="addTodo" />
				<MyList :todoList="todoList" :deleteTodo="deleteTodo" :checkedTodo="checkedTodo" />
				<MyFooter :todoList="todoList" :deleteDone="deleteDone" :checkedAllTodo="checkedAllTodo" />
			</div>
		</div>
	</div>
</template>

<script>
import { nanoid } from 'nanoid'
import MyHeader from './components/MyHeader'
import MyList from './components/MyList'
import MyFooter from './components/MyFooter.vue'

const todoList = [
	{ id: nanoid(), title: '吃饭', done: true },
	{ id: nanoid(), title: '睡觉', done: false },
	{ id: nanoid(), title: '打代码', done: true },
]
export default {
	name: 'App',
	components: { MyHeader, MyList, MyFooter },
	data() {
		return {
			todoList,
		}
	},
	methods: {
		addTodo(todo) {
			this.todoList.unshift(todo)
		},
		deleteTodo(id) {
			this.todoList = this.todoList.filter(todo => todo.id !== id);
		},
		checkedTodo(id) {
			this.todoList.forEach(todo => {
				if (todo.id === id) {
					todo.done = !todo.done
				}
			})
		},
		deleteDone() {
			this.todoList = this.todoList.filter(todo => !todo.done)
		},
		checkedAllTodo(done) {
			this.todoList.forEach(todo => {
				todo.done = done;
			})
		}
	}
}
</script>

<style>
/*base*/
body {
	background: #fff;
}

.btn {
	display: inline-block;
	padding: 4px 12px;
	margin-bottom: 0;
	font-size: 14px;
	line-height: 20px;
	text-align: center;
	vertical-align: middle;
	cursor: pointer;
	box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
	border-radius: 4px;
}

.btn-danger {
	color: #fff;
	background-color: #da4f49;
	border: 1px solid #bd362f;
}

.btn-danger:hover {
	color: #fff;
	background-color: #bd362f;
}

.btn:focus {
	outline: none;
}

.todo-container {
	width: 600px;
	margin: 0 auto;
}

.todo-container .todo-wrap {
	padding: 10px;
	border: 1px solid #ddd;
	border-radius: 5px;
}
</style>
