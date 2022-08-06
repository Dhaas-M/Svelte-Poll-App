<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
    export let items;
    export let active_item;
</script>

<nav>
    <ul>
        {#each items as item}
            <li 
                class:active={item === active_item}
                on:click={() => dispatch('tabChange', item)}
            >
                {item}
            </li>
        {/each}
    </ul>
</nav>

<style>
    nav li{
        padding: 5px;
        margin: 5px;
        cursor: pointer;
    }
    nav ul{
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.5em;
        list-style-type: none;
    }
    .active{
        color: rgb(202, 83, 83);
        text-decoration: underline;
    }
</style>