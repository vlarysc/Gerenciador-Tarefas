<template>
	<div id="app">		
		<h1 class="perfect">Tarefas</h1>
		<br>
		<br>
		<TasksProgress :progress="progress" />
		<NewTask @taskAdded="addTask" />
		<TaskGrid @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState" :tasks="tasks" />
	</div>

</template>

<script>
import TasksProgress from './components/TasksProgress'
import NewTask from './components/NewTask'
import TaskGrid from './components/TaskGrid'

export default {
	components: { TaskGrid, NewTask, TasksProgress },
	data() {
		return {
			tasks: []
		}
	},
	computed: {
		progress() {
			const total = this.tasks.length
			const done = this.tasks.filter(t => !t.pending).length
			return Math.round(done / total * 100) || 0
		}
	},
	watch: {
		tasks: {
			deep: true,
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks))
			}
		}
	},
	methods: {
		addTask(task) {
			const sameName = t => t.name === task.name
			const reallyNew = this.tasks.filter(sameName).length == 0
			if(reallyNew) {
				this.tasks.push ({
					name: task.name,
					pending: task.pending || true
				})
			}
		},
		deleteTask(i) {
			this.tasks.splice(i, 1)
		},
		toggleTaskState(i) {
			this.tasks[i].pending = !this.tasks[i].pending
		}
	},
	created() {
		const json = localStorage.getItem('tasks')
		this.tasks = JSON.parse(json) || []
	}

}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 600;
		font-size: 3rem;
	}
	.perfect {
		color: #a8a7aa;  /* fallback for old browsers */
color: -webkit-linear-gradient(to right, #E7E9BB, #403B4A);  /* Chrome 10-25, Safari 5.1-6 */
color: linear-gradient(to right, #e1e4a8, #9479cc); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

	}

	
</style>
