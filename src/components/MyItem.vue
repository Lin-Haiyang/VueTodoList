<template>
	<li>
		<label>
			<input type="checkbox" :checked="todo.done" @change="handleCheckedTodo(todo.id)" />
			<span v-show="!isEdit">{{ todo.title}}</span>
			<input
				v-show="isEdit"
				ref="inputTitle"
				type="text"
				v-model="editTitle"
				@blur="handleBlur(todo.id, $event)"
			>
		</label>
		<button class="btn btn-danger" @click="handleDeleteTodo(todo.id)" >删除</button>
		<button v-show="!isEdit" class="btn btn-normal" @click="handleEditTodo(todo)" >编辑</button>
	</li>
</template>

<script>
	export default {
		name:'MyItem',
		props:['todo'],
		data() {
			return {
				editTitle: '',
				isEdit: false,
			}
		},
		methods: {
			handleDeleteTodo(id) {
				if(confirm(`确定删除【${this.todo.title}】事情吗？`)){
					//通知App组件将对应的todo对象删除
					this.$bus.$emit('deleteTodo', id);
				}
			},
			handleCheckedTodo(id) {
				this.$bus.$emit('checkedTodo', id);
			},
			handleEditTodo() {
				this.isEdit = !this.isEdit;
				this.editTitle = this.todo.title;
				this.$nextTick(function(){
					this.$refs.inputTitle.focus()
				})
			},
			handleBlur(id, e) {
				this.isEdit = !this.isEdit;
				if (e.target.value) {
					this.$bus.$emit('editTodo', id, e.target.value);
				} else {
					return
				}
			}
		}
	}
</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
	}

	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}

	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}

	li:before {
		content: initial;
	}

	li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>