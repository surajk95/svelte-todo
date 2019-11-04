<script>
export let tasks=[], type, completed, notcompleted, deleteTask;
</script>

{#each tasks as task}
	<div class="tasks">
		{task.title}
        <button on:click={()=>deleteTask(task.id)}>Delete</button>
		{#if type==='incomplete'}
            <button on:click={()=>completed(task.id)}>Done</button>
        {:else}
            <button on:click={()=>notcompleted(task.id)}>Not Done</button>
        {/if}
	</div>
{/each}

<style>
    .tasks {
            text-align: left;
            width: 300px;
            margin: 20px auto;
            border: solid 1px grey;
            padding : 20px 30px;
        }
    button {
        float: right;
        background-color: white;
        color: black;
        border: none;
        outline: none;
        margin: -5px 0 0 10px;
    }
</style>