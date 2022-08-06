<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
    let fields = {question:'', ansA: '', ansB: ''}
    const handleSubmit = () => {
        let poll = {...fields, votesA: 0, votesB: 0, id: Math.random()}
        dispatch('add', poll)
    }
</script>

<form action="" on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="Question" bind:value={fields.question} required>
    <input type="text" placeholder="Answer-A" bind:value={fields.ansA} required>
    <input type="text" placeholder="Answer-B" bind:value={fields.ansB} required>
    <button>Add Your Poll</button>
</form>

<style>
    form{
        width: 400px;
        text-align: center;
        margin: 0 auto;
    }
    input{
        width: 100%;
    }
</style>