<template>
	<div class="todo-footer" v-show="todoList.length">
		<label>
			<input type="checkbox" v-model="isAll"  />
		</label>
		<span> <span>已完成{{ dones }}</span> / 全部{{ total }}</span>
		<button class="btn btn-danger" @click="handleDeleteDone">清除已完成任务</button>
	</div>
</template>

<script>
export default {
	name: "MyFooter",
	props: ["todoList", 'deleteDone', 'checkedAllTodo'],
	computed: {
		total() {
			return this.todoList.length;
		},
		dones() {
			return this.todoList.reduce((pre, current) => {
				return pre + (current.done ? 1 : 0);
			}, 0)
		},
		isAll: {
			get() {
				return this.dones === this.total;
			},
			set(value) {
				this.$emit('checkedAllTodo', value);
			}
		}
	},
	methods: {
		handleDeleteDone() {
			if (this.dones) {
				if (confirm(`确定删除${this.dones}个已完成事情吗？`)) this.$emit('deleteDone');
			} else {
				alert('目前没有已完成的事情！')
			}
		}
	}
};
</script>

<style scoped>
/*footer*/
.todo-footer {
	height: 40px;
	line-height: 40px;
	padding-left: 6px;
	margin-top: 5px;
}

.todo-footer label {
	display: inline-block;
	margin-right: 20px;
	cursor: pointer;
}

.todo-footer label input {
	position: relative;
	top: -1px;
	vertical-align: middle;
	margin-right: 5px;
}

.todo-footer button {
	float: right;
	margin-top: 5px;
}
</style>