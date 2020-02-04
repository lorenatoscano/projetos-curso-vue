<template>
	<div id="app">
		<h1>Tarefas</h1>
		<task-progress :progress="progress"/>
		<new-item @taskAdded="addTask"/>
		<task-list :tasks="tasks"
			@taskDeleted="deleteTask"
			@taskStateChanged="toggleTaskState" />
	</div>
</template>

<script>
import TaskList from './components/TaskList.vue'
import NewItem from './components/NewItem.vue'
import TaskProgress from './components/TaskProgress.vue'
export default {
	components: { TaskList, NewItem, TaskProgress},
	data() {
		return {
			tasks: []
		}
	},
	computed: {
		progress() {
			const total = this.tasks.length;
			//Pega o tamanho do array formado pelas tarefas concluídas
			const done = this.tasks.filter(t => !t.pending).length;
			return Math.round(done/total * 100) || 0;
		}
	},
	methods: {
		addTask(newTask) {
			//Verifica se a tarefa já existe
			//Filtra todas as tasks com o mesmo nome
			//Se o array final for vazio, reallyNew = true
			const sameName = t => t.name === newTask.name;
			const reallyNew = this.tasks.filter(sameName).length == 0
			
			if (reallyNew) {
				//Adiciona a nova tarefa no array
				this.tasks.push({
					name: newTask.name,
					pending: newTask.pending || true
				})
			}
		},
		deleteTask(task) {
			const i = this.tasks.indexOf(task);
			//Exclui um elemento a partir do indice i
			if (i >= 0) this.tasks.splice(i, 1);
		},
		toggleTaskState(i) {
			this.tasks[i].pending = !this.tasks[i].pending;
		}
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(3, 35, 56), rgb(30, 141, 197));
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
		font-weight: 300;
		font-size: 3rem;
	}
</style>
