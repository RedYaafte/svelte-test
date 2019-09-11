<script>
    import { onMount } from 'svelte';
    let morty = "Rick and Moty";
    let item;

    async function rick() {
        item = await fetch(`https://rickandmortyapi.com/api/character/`).then(r => r.json());
        console.log(item)
    }
    onMount(rick);
</script>

<main>
    {#if item}
        {#each item.results as result}
            <div class="card">
                <h2>{result.name}</h2>
                <img src={result.image} alt="{result.name}">
                <p><small><strong>Status:</strong> {result.status} <strong>Species:</strong> {result.species}</small></p>
            </div>
        {/each}
    {:else}
        <h1>No no no has dicho las palabras magicas!!</h1>
    {/if}
</main>

<style>
    h2 {
        color: #000;
    }
    .card {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    img {
        border-radius: 50%;
        cursor: pointer;
    }
    img:hover {
        transition: all .5s;
        transform: translateY(-5px);
    }
    img:hover h2 {
        transition: all .5s;
        color: rgb(237, 6, 6);
    }
</style>