<script>
	import { Router, Link, Route } from 'svelte-routing';
	import Blog from './components/Blog.svelte';
	import Home from './components/Home.svelte';
	export let name;
	export let url = "";
</script>

<Router url="{url}">
  <nav>
    <Link to="/">Home</Link>
    <Link to="blog">Blog</Link>
  </nav>
  <div>
    <Route path="/"><Home /></Route>
    <Route path="blog" component="{Blog}" />
  </div>
</Router>

<style>
	h1 {
		color: purple;
	}
  nav {
    padding: 20px;
    background-color: lightgray;
  }
</style>

