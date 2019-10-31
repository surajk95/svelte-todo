<script>
	let name = 'world';
	let title = '';
	let tasks = [];
	$: completedTasks = tasks.filter(item => item.completed==true);
	$: incompleteTasks = tasks.filter(item => item.completed==false);
	let addTask = () => {
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
	<button type="submit">Submit</button>
</form>
<h2>To Do</h2>
{#each incompleteTasks as task}
	<div class="tasks">
		{task.title}
		<button on:click={()=>completed(task.id)}>Done</button>
		<button on:click={()=>deleteTask(task.id)}>Delete</button>
	</div>
{/each}
<h2>Done</h2>
{#each completedTasks as task}
	<div class="tasks">
		{task.title}
		<button on:click={()=>notcompleted(task.id)}>Not Done</button>
		<button on:click={()=>deleteTask(task.id)}>Delete</button>
	</div>
{/each}


<style>
	h1, div {
		
	}
	h2 {
		text-decoration: underline;
	}
	.tasks {
		text-align: left;
		width: 200px;
		margin: 20px auto;
		border: solid 1px grey;
		padding : 10px 30px;
	}
</style>