<script>
	import { draggable } from "$lib/dnd";
    let date = new Date();
    let year = new Intl.DateTimeFormat('en', { year: 'numeric' }).format(date);
    let month = new Intl.DateTimeFormat('en', { month: 'short' }).format(date);
    let day = new Intl.DateTimeFormat('en', { day: '2-digit' }).format(date);

    const filters = ["Todos","Activos","Completados"]
    let filterselected = "Todos"

</script>
<div class="container" use:draggable={"test"}>
    <div class="title">
        {new Date().toDateString()}
    </div>
    <div class="task">
        <span>5 tasks</span>
        <div class="task-status">
            {#each filters as filter}
            <button on:click={()=>{
                filterselected = filter
            }} class={filter == filterselected ? 'isactive' : ''}>{filter}</button>
            {/each}
        </div>
    </div>
    <input class="new-todo" type="text" placeholder="Nueva tarea">
</div>
<div class="todos">
    <div class="no-todos">
        Sin pendientes
    </div>
</div>
<style>
    @import url('https://fonts.googleapis.com/css?family=DM+Sans:400,500,700&display=swap');
    * {
        font-family: 'DM Sans', sans-serif;
    }
    .container{
        width: 450px;
        background-color: whitesmoke;
        border-radius: 16px 16px 0 0;
        padding: 15px 15px 0 15px;
        font: 'DM Sans', sans-serif;
    }
    .title{
        font-size: 20px;
        font-weight: 600;
        color: #555555;
    }
    .task{
        display: grid;
        grid-template-columns: 50% 50%;
        & > span{
            color: #949494;
        }
    }
    .task-status{
        justify-self: right;
        & > button{
            border-style: none;
            cursor: pointer;
            border-radius: 15px;
            height: 25px;
        }
        & > .isactive{
            background-color: #7996a5;
            color: #fff;
        }
    }
    .new-todo{
        margin-top: 20px;
        width: 100%;
        outline: none;
        border-style: none;
        border-bottom: solid 1px lightgray;
        padding: 10px 0px;
        background-color: whitesmoke;
    }
    .todos{
        width: 480px;
        height: 150px;
        background-color: whitesmoke;
        border-radius: 0 0 16px 16px;
    }
    .no-todos{
        width: 100%;
        height: 100%;
        font-weight: bold;
        font-size: larger;
        opacity: .3;
    }
</style>