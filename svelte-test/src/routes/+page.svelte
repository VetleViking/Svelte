<script>
    import "../app.css";
    let count = 0;
    let navn = "Svelte";
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<p>{navn}</p>

<button on:click={() => count += 1}>Click me</button>
<p>{count}</p>

<a href="/ovn">Ovn</a>

