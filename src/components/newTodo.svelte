<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { generateId } from '$lib/utils';
	const dispatch = createEventDispatcher();

	let name: string | null = null;
	let date: Date | null = null;

	function create() {
		name = name?.trim() ?? null;
		if (date == null && name == null) {
			alert('Rellene los datos');
		} else {
			dispatch('create', {
				id: generateId(),
				name,
				date,
				tasks: []
			});
		}
	}
	function close() {
		dispatch('close');
	}
</script>

<div class="form">
	<label for="nombre">Nombre</label>
	<input bind:value={name} type="text" id="nombre" />
	<label for="fecha">Fecha</label>
	<input bind:value={date} type="date" id="fecha" />
	<button
		on:click={() => {
			create();
		}}>Agregar</button
	>
	<button class="close" on:click={close}>X</button>
</div>

<style>
	.form {
		display: flex;
		flex-direction: column;
		max-width: 50%;
		min-width: 320px;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 9999;
		background-color: whitesmoke;
		border-radius: 5px;
		padding: 25px;
		box-shadow: 4px 3px 5px -3px rgba(0, 0, 0, 0.76);
		-webkit-box-shadow: 4px 3px 5px -3px rgba(0, 0, 0, 0.76);
		-moz-box-shadow: 4px 3px 5px -3px rgba(0, 0, 0, 0.76);
		& > button {
			margin-top: 15px;
			background-color: lightblue;
			border-width: 0.5px;
		}
	}
	.close {
		position: absolute;
		top: -5px;
		right: 10px;
		background-color: #eb1f1f !important;
		font-weight: bolder;
	}
</style>
