<script lang="ts">
	import TodoList from "../components/TodoList.svelte";


</script>
<div>
	
	<TodoList pending={[{id:3,status:false,task:" 1.  pending"}]} completed={[{id:0,status:true,task:"2. list Todo done"},{id:2,status:true,task:"3. list Todo done"}]}></TodoList>
</div>

<style>
	div{
		width: 100vw;
		height: 100vh;
		display: flex;
		justify-content:center ;
	}
</style>