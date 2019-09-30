<script>
  import { onMount } from 'svelte';

  let title = "Rick and Moty";
  let item;

  async function rick() {
    item = await fetch(`https://rickandmortyapi.com/api/character/`).then(r => r.json());
  }
  onMount(rick);
</script>


<main>
  <h1>{title}</h1>
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
    <img src="https://pa1.narvii.com/6362/3bb30f21cd66eb5f5fb6c636fc77f0a36b842f6f_hq.gif" alt="No no no has dicho las palabras magicas!!">
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