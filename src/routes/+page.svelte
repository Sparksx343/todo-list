<script lang="ts">
	import { onMount } from 'svelte';
	import Card from '../components/Card.svelte';
	import NewTodo from '../components/newTodo.svelte';

	let todos = [
		{ id: generateId(), text: 'texto prueba2', finished: false },
		{ id: generateId(), text: 'texto prueba343', finished: true },
		{ id: generateId(), text: 'texto pruebasdf', finished: false }
	];

	let newTodo = false;
	let data: any[] = [];
	function generateId() {
		return Math.random().toString(16).slice(2);
	}

	onMount(() => {
		const retrieve = localStorage.getItem('data');
		if (retrieve === null) return;
		data = JSON.parse(retrieve);
	});

	function addTodo(todo: any) {
		console.log(todo);
		data.push(todo.detail);
		data = [...data];
		newTodo = false;
	}
</script>

<body>
	{#if newTodo}
		<NewTodo
			on:create={addTodo}
			on:close={() => {
				newTodo = false;
			}}
		/>
	{/if}
	<div class="container">
		{#each data as todo}
			<Card />
		{/each}
		{#if data.length == 0}
			<div class="no-todos">
				<span>Sin pendientes</span>
			</div>
		{/if}
	</div>
	<button
		class="add"
		on:click={() => {
			newTodo = true;
		}}>+</button
	>
</body>

<style>
	@import url('https://fonts.googleapis.com/css?family=DM+Sans:400,500,700&display=swap');
	* {
		font-family: 'DM Sans', sans-serif;
		user-select: none;
	}
	body {
		background-image: linear-gradient(
			102.7deg,
			rgba(253, 218, 255, 1) 8.2%,
			rgba(223, 173, 252, 1) 19.6%,
			rgba(173, 205, 252, 1) 36.8%,
			rgba(173, 252, 244, 1) 73.2%,
			rgba(202, 248, 208, 1) 90.9%
		);
		background-attachment: fixed;
		background-repeat: no-repeat;
		background-size: cover;
	}
	.container {
		display: grid;
		gap: 25px;
		grid-template-columns: repeat(auto-fit, minmax(470px, 10px));
		padding-bottom: 25px;
	}
	.add {
		position: fixed;
		bottom: 25px;
		right: 25px;
		border-radius: 50%;
		height: 55px;
		width: 55px;
		border-style: none;
		cursor: pointer;
		background-color: #6bb2ca;
		color: white;
		font-weight: bold;
		font-size: large;
	}
	.add:active {
		transform: scale(0.9);
	}
	.no-todos {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-weight: bold;
		font-size: 50px;
		opacity: 0.5;
	}
</style>
