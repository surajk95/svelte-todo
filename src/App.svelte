<script>
	import Tasks from './components/tasks.svelte';

	let name = 'world';
	let title = '';
	let tasks = [];
	$: completedTasks = tasks.filter(item => item.completed==true);
	$: incompleteTasks = tasks.filter(item => item.completed==false);
	let addTask = () => {
		if(title.trim() === '')
			return;
		let task = {
			title,
			id: tasks.length,
			completed: false,
		}
		tasks[tasks.length] = task;
		title = '';
	}

	let deleteTask = (id) => {
		tasks = tasks.filter(task => task.id!==id);
	}

	let completed = (id) => {
		tasks = tasks.map(task => task.id===id?{...task,completed: true}:task);
	}

	let notcompleted = (id) => {
		tasks = tasks.map(task => task.id===id?{...task,completed: false}:task);
	}

</script>

<h1>Helou {name}!</h1>

<form on:submit|preventDefault={addTask} >
	<input type="text" bind:value={title} placeholder="Type something..." />
	<button type="submit">Add</button>
</form>

{#if incompleteTasks.length>0}
<h2>To Do</h2>
<Tasks tasks={incompleteTasks} {deleteTask} {completed} type="incomplete"/>
{/if}

{#if completedTasks.length>0}
<h2>Done</h2>
<Tasks tasks={completedTasks} {deleteTask} {notcompleted} type="complete"/>
{/if}

<style>
	:global(body) {
		background-color: black;
		color: white;
		text-align: center;
	}
	h1, div {
		
	}
	h2 {
		text-decoration: underline;
	}
	input {
		outline: none;
		border: none;
		border-bottom: 2px solid white;
		padding-bottom: 5px;
		color: white;
		background-color: black;
		margin: 0 20px;
	}

	button {
		background-color:black;
		color: white;
		border: 2px solid white;
	}
	
</style>