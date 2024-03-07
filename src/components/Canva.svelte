<script>
    import {dropzone} from '$lib/dnd'
</script>
<div class="container">
    <div use:dropzone class="column">as</div>
    <div use:dropzone class="column">asd</div>
    <div use:dropzone class="column">sda</div>
</div>
<style>
    .container{
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        margin: auto;
        width: 70vw;
        min-width: 400px;
        height: 80vh;
        border-radius: 15px;
        background-color: whitesmoke;
        & > *{
            margin: 10px;
            padding: 10px;
            background-color: lightgray;
        }
    }
    @media only screen and (max-width: 500px) {
  .container {
    background-color: lightblue;
  }
}

.column:global(.droppable){
    outline: 0.1rem solid red;
    outline-offset: 0.25rem;
}
.column:global(.droppable) * {
    pointer-events: none;
}
</style>