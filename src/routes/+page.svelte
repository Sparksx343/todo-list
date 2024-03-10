<script>
	import {onMount} from 'svelte'
	import Card from "../components/Card.svelte";

	onMount(()=>{
		const data = localStorage.getItem('todos');
		console.log(data);
	})
</script>
<body>
	<div class="container">
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
		<Card />
	</div>
		<button class="add">+</button>
</body>

<style>
body {
	 background-image: linear-gradient(102.7deg, rgba(253, 218, 255, 1) 8.2%, rgba(223, 173, 252, 1) 19.6%, rgba(173, 205, 252, 1) 36.8%, rgba(173, 252, 244, 1) 73.2%, rgba(202, 248, 208, 1) 90.9%);
	 background-attachment: fixed;
	 background-repeat: no-repeat;
	 background-size: cover;
}
.container{
	display: grid;
	gap: 25px;
	grid-template-columns: repeat(auto-fit, minmax(470px, 10px));
	padding-bottom: 25px;
}
.add{
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
.add:active{
	transform: scale(.9);
}
</style>