<script lang="ts">
	import type { ITodoList } from './todoList';
	export let pending: ITodoList[] = [];
	export let completed: ITodoList[] = [];
	let inp = '';
	function changeTodo(
		e: MouseEvent & { currentTarget: EventTarget & HTMLInputElement },
		id: number,
		idx: number,
		select: 'pending' | 'done'
	) {
		if (select === 'pending') {
			pending[idx].status = true;
			completed.push(pending[idx]);
			pending.splice(idx, 1);
			pending = pending;
			completed = completed;
			console.log('pending', pending, completed);
		} else {
			completed[idx].status = false;
			pending.push(completed[idx]);
			completed.splice(idx, 1);
			pending = pending;
			completed = completed;
			console.log('completed', pending, completed);
		} // todos = todos;
	}

	function deteteIdx(select: 'pending' | 'done', idx: number) {
		if (select === 'pending') {
			pending.splice(idx, 1);
			pending = pending;

			console.log('pending', pending, completed);
		} else {
			completed.splice(idx, 1);

			completed = completed;
			console.log('completed', pending, completed);
		} // todos = todos;
	}
</script>

<div class="main">
	<div class="wrapper">
		<p class="title-p">Pending todos</p>
		<div class="todos">
			{#each pending as todo, idx}
			{#if todo.status==false}
				
			<div class="pending">
				<span class="task"> {todo.task} </span>
				<div class="box">
					<center>
					<input
					type="checkbox"
					bind:checked={pending[idx].status}
							on:click={(e) => {
								changeTodo(e, todo.id, idx, 'pending');
							}}
							class="icon"
							/><button
							on:click={() => {
								deteteIdx('pending', idx);
							}}>Delete</button
						>
					</center>
					</div>
				</div>
				{/if}
				{/each}
				<div class="add">
					<input type="text" name="todo" maxlength="35" bind:value={inp} id="" />
					<button
					on:click={() => {
						pending.push({ id: 1, status: false, task: inp });
						inp = '';
						$: pending = pending;
					}}
				>
					Add Pending</button
				>
			</div>
		</div>
	</div>
	<div class="wrapper">
		<p class="title-d">Completed Todos</p>
		<div class="todos">
			{#each completed as todo, idx}
				<div class="done">
					<span class="task">{todo.task}</span>
					<div class="box">
						<input
							type="checkbox"
							bind:checked={completed[idx].status}
							on:click={(e) => {
								changeTodo(e, todo.id, idx, 'done');
							}}
							class="icon"
						/><button
							on:click={() => {
								deteteIdx('done', idx);
							}}>Delete</button
						>
					</div>
				</div>
			{/each}
		</div>
	</div>
</div>

<style>
	:global(body){
		background-color: #0f0563;
	
	}
	.main{
		background-color: aliceblue;
		border-radius: 20px;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		height: 100px;

	}
	.wrapper {
		padding: 20px;
		border: 2px solid rgb(122, 124, 3);
		border-radius: 25px;
		box-shadow: inset #0f0f0f;
		display: flex;
		row-gap: 20px;
min-height:100px;
		column-gap: 20px;
		flex-direction: column;
		/* justify-content: center;
		align-items: center; */
		margin: 15px;
		background-color: rgb(252, 255, 73);
	}
	.todos {
		min-width: 20vw;
		
		display: flex;
		flex-direction: column;
		flex-wrap: wrap;

		gap: 10px;
	}
	.done {
	
	}
	.pending {
		
	}
	.title-p {
	}
	.title-d {
	
	}

	.done,
	.pending {
		border: 2px solid #cfaa02;
		padding: 5px;
		background-color: #ffd000;
		display: flex;
		gap: 15px;
		justify-content: space-between;
		border-radius: 10px;
		width: 20vw;
		font-size: x-small;
	}
	.add {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}
	.add input,
	.add button {
		overflow-wrap: break-word;
		width: 20vw;
		border-radius: 25px;
		padding: 10px;
		text-align: center;
		justify-content: center;
		word-wrap: break-word;
	}
	.box {
		display: flex;
		gap: 5px;
	}
	 button{
		border-radius: 25px;
		padding: 5px;
		background-color:tomato ;
		
	}
	
</style>
