<script>
	// @ts-nocheck
	const filters = ['Todos', 'Pendientes', 'Completados'];
	let filterselected = 'Todos';
	let newTask = '';

	let todos = [
		{ id: generateId(), text: 'texto prueba2', finished: false },
		{ id: generateId(), text: 'texto prueba343', finished: true },
		{ id: generateId(), text: 'texto pruebasdf', finished: false }
	];
	let filtered = todos;

	function generateId() {
		return Math.random().toString(16).slice(2);
	}

	function getFiltered() {
		if (filterselected == 'Todos') {
			filtered = todos;
		}
		if (filterselected == 'Pendientes') {
			filtered = todos.filter((task) => task.finished === false);
		}
		if (filterselected == 'Completados') {
			filtered = todos.filter((task) => task.finished === true);
		}
	}

	function getIndexOfTask(id) {
		const idx = todos.map((e) => e.id).indexOf(id);
		return idx;
	}

	function deleteTask(id) {
		const idx = getIndexOfTask(id);
		todos.splice(idx, 1);
		todos = [...todos];
		getFiltered();
	}
</script>

<div class="wrapper">
	<div class="container">
		<div class="title">
			Ajas ajas
			<div class="date">
				{new Date().toDateString()}
			</div>
		</div>
		<div class="task">
			<span>{todos.length} tareas</span>
			<div class="task-status">
				{#each filters as filter}
					<button
						on:click={() => {
							filterselected = filter;
							getFiltered();
						}}
						class={filter == filterselected ? 'isactive' : ''}>{filter}</button
					>
				{/each}
			</div>
		</div>
		<input
			bind:value={newTask}
			class="new-todo"
			type="text"
			on:keyup={(e) => {
				if (e.key == 'Enter') {
					if (newTask == '') return;
					todos.push({ id: generateId(), text: newTask, finished: false });
					todos = [...todos];
					newTask = '';
					getFiltered();
				}
			}}
			placeholder="Nueva tarea"
		/>
	</div>
	<div class="todos">
		{#if filtered.length > 0}
			{#each filtered as todo, idx}
				<div class="todo">
					<input
						type="checkbox"
						bind:checked={todo.finished}
						on:change={(e) => {
							todo.finished = e.target.checked;
							getFiltered();
						}}
						id={todo.id}
					/>
					<label class={todo.finished ? 'finished' : ''} for={todo.id}>{todo.text}</label>
					<button on:click={deleteTask(todo.id)} type="button">🗑</button>
				</div>
			{/each}
		{:else}
			<div class="no-todos">
				Sin {filterselected}
			</div>
		{/if}
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css?family=DM+Sans:400,500,700&display=swap');
	* {
		font-family: 'DM Sans', sans-serif;
		user-select: none;
	}
	.container {
		width: 450px;
		background-color: whitesmoke;
		border-radius: 16px 16px 0 0;
		padding: 15px 15px 0 15px;
		font: 'DM Sans', sans-serif;
	}
	.title {
		display: flex;
		align-items: end;
		font-size: 20px;
		font-weight: 600;
		color: #555555;
		& > .date {
			margin-left: 15px;
			font-size: 15px;
		}
	}
	.task {
		display: grid;
		grid-template-columns: 30% 70%;
		& > span {
			color: #949494;
		}
	}
	.task-status {
		justify-self: right;
		& > button {
			border-style: none;
			cursor: pointer;
			border-radius: 15px;
			height: 25px;
			margin: 0 5px;
		}
		& > .isactive {
			background-color: #7996a5;
			color: #fff;
		}
	}
	.new-todo {
		margin-top: 20px;
		width: 100%;
		outline: none;
		border-style: none;
		border-bottom: solid 1px lightgray;
		padding: 10px 0px;
		background-color: whitesmoke;
	}
	.todos {
		display: block;
		width: 480px;
		padding-top: 15px;
		padding-bottom: 15px;
		background-color: whitesmoke;
		border-radius: 0 0 16px 16px;
	}
	.todo {
		display: grid;
		grid-template-columns: 10% 80% 10%;
		padding-right: 15px;
		margin-bottom: 5px;
		& > button {
			color: red;
		}
		& > * {
			cursor: pointer;
			user-select: none;
		}
	}
	.finished {
		color: #929292;
		text-decoration-line: line-through;
	}
	.no-todos {
		width: 100%;
		height: 100%;
		font-weight: bold;
		font-size: larger;
		opacity: 0.3;
		display: flex;
		justify-content: center;
		align-items: center;
	}
</style>
