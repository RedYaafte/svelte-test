<script>
  import { onMount } from 'svelte';
  import { navigate } from "svelte-routing";

  let item;
  let post;
  let error;

  async function rick() {
    item = await fetch('http://localhost:3004/posts').then(r => r.json());
  }
  onMount(rick);

  async function sendData(data) {
    post = await fetch('http://localhost:3004/posts',
      {
        headers: { "Content-Type": "application/json" },
        method: 'POST',
        body: JSON.stringify(data)
      }
    )

    if (post.status == 201) {
      navigate("/", { replace: true });
    } else {
      error = '¡Ops you have error!'
    }
  }

  function handleSubmit(event) {
    event.preventDefault();
    console.log(event);
    console.log(event.target[0].value);
    console.log(event.target[1].value);
    console.log(event.target[2].value);
    let data = {
      "title": event.target[0].value,
      "body": event.target[1].value,
      "author": event.target[2].value
    }
    sendData(data)
  }
</script>


{#if error}
  <span class="error">{error}</span>
{/if}
<form on:submit={handleSubmit}>
  <input type="text" placeholder="title" name="title"> <br>
  <textarea rows="4" cols="50" name="body"> </textarea> <br>
  <input type="text" placeholder="author" name="author"> <br>
  <button type="submit">Create</button>
</form>

<hr>
{#if item}
  {#each item as post}
    <div>
      <h2>{post.title}</h2>
      <p>{post.body}</p>
      <div class="text-right"><small>{post.author}</small></div>
    </div>
  {/each}
{/if}


<style>
form {
  margin-top: 20px;
  margin-bottom: 20px;
}
div {
  border-bottom: 1px solid lightgray;
}
p {
  margin: 0;
}
small {
  color: grey;
}
.error {
  color: red;
}
.text-right {
  text-align: right;
}
</style>