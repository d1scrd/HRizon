<script>
    import Router from 'svelte-spa-router';
    import routes from "./routes/routes";
    import Navbar from './components/navbar.svelte';
</script>

<div class="app-container">
    <Navbar />
    <Router {routes} />
</div>

<style>
    .app-container {
        display: flex;
    }
</style>
