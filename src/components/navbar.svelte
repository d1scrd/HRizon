<script>
    import { location } from "svelte-spa-router";
    import { Icon, HomeModern, GlobeAlt } from "svelte-hero-icons";
  
    let routes = [
        { name: "Home", route: "#/home", icon: HomeModern },
        {name:"Tree", route: '#/tree', icon: GlobeAlt }
        // Add other routes here as needed
    ];
</script>

<div class="sidebar">
    <div class="logo">
        <a href="/">MyApp</a>
    </div>
    <div class="nav-links">
        {#each routes as route}
            <a href={route.route} class="{ $location === route.route ? 'active' : '' }">
                <Icon src={route.icon} size="24" class="icon"/>
                <span class="nav-text">{route.name}</span>
            </a>
        {/each}
    </div>
</div>

<style>
    .sidebar {
        height: 100vh;
        width: 200px;
        background-color: #333;
        color: white;
        display: flex;
        flex-direction: column;
        padding: 1rem;
    }

    .logo a {
        color: white;
        text-decoration: none;
        font-size: 1.5rem;
        font-weight: bold;
        margin-bottom: 2rem;
    }

    .nav-links {
        display: flex;
        flex-direction: column;
    }

    .nav-links a {
        color: white;
        text-decoration: none;
        margin-bottom: 1rem;
        display: flex;
        align-items: center;
        transition: color 0.3s;
    }

    .nav-links a:hover {
        color: #ccc;
    }

    .nav-links a.active {
        font-weight: bold;
        border-right: 4px solid #fff;
    }

    .icon {
        margin-right: 10px;
    }

    .nav-text {
        margin-left: 10px;
    }
</style>
