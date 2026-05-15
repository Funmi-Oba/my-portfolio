<script>
  import './layout.css';
  import Navbar from '$lib/components/Navbar.svelte';

  let { children } = $props();
</script>

<div id="app" style="background-color: #161622; min-height: 100vh;">
  <Navbar />
  <main>
    {@render children()}
  </main>
</div>