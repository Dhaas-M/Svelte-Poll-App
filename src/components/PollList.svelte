<script>
    import PollDetails from "./PollDetails.svelte";
    export let polls=[];
</script>

<div class='grid'>
    {#each polls as poll (poll.id)}
        <div>
            <PollDetails {poll} on:vote />
        </div>
    {:else}
        <p>No Polls are Here</p>
    {/each}
</div>

<style>
    .grid{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-row: 20px;
    }
</style>