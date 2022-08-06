<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher()
    import Card from '../shared/Card.svelte'
    export let poll;

    $: totalVotes = poll.votesA + poll.votesB
    $: percentA = Math.floor(100 / totalVotes * poll.votesA)
    $: percentB = Math.floor(100 / totalVotes * poll.votesB)

    const handleClick = (option, id) => {
        dispatch('vote', {option, id})
    }
</script>

<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>{ totalVotes } people voted</p>
        <div class="answer" on:click={() => handleClick('a', poll.id)}>
            <div class='percent percent-A' style="width: {percentA}%"></div>
            <span>{ poll.ansA} ({ poll.votesA })</span>
        </div>
        <div class="answer" on:click={() => handleClick('b', poll.id)}>
            <div class='percent percent-B' style="width: {percentB}%"></div>
            <span>{ poll.ansB } ({ poll.votesB })</span>
        </div>
    </div>
</Card>

<style>
    .answer{
        background-color: #fafafa;
        margin: 10px auto;
        padding: 5px;
        cursor: pointer;
        position: relative;
    }
    .answer:hover{
        opacity: 0.6;
    }
    .percent{
        height: 100%;
        position: absolute;
        box-sizing: border-box;
        transition: 0.1ms ease;
    }
    .percent-A{
        border-left: 4px solid #d91b42;
        background-color: rgba(217,27,66,0.2);
    }
    .percent-B{
        border-left: 4px solid #45c496;
        background-color: rgba(69,196,150,0.2);
    }
</style>