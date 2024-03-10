<script>
    import Navbar from '$lib/components/Navbar.svelte';
    import { onMount } from 'svelte';

    let loves = 0;
    let favorites = 0;
    let id = null;
    let title = ""; 
    let desc = ""; 
    
    function getSearchParams() {
        const params = new URLSearchParams(window.location.search);
        id = params.get('id');
    }
    
    async function fetchLoves(projectId) {
        try {
            const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/projects/${projectId}`);
            const datalove = await response.json();
            loves = datalove.stats.loves;
        } catch (error) {
            console.error("Error fetching data:", error);
        }
    }
    async function fetchStars(projectId) {
        try {
            const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/projects/${projectId}`);
            const datafav = await response.json();
            favorites = datafav.stats.favorites;
        } catch (error) {
            console.error("Error fetching data:", error);
        }
    }
    
    async function fetchName(projectId) {
        try {
            const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/projects/${projectId}`);
            const dataname = await response.json();
            title = dataname.title;
        } catch (error) {
            console.error("Error fetching data:", error);
        }
    }
    
    async function fetchDesc(projectId) {
        try {
            const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/projects/${projectId}`);
            const datadesc = await response.json();
            desc = datadesc.description.replace(/https:\/\/scratch\.mit\.edu\/projects\/(\d+)/g, '<a href="https://scroll3.vercel.app/view?id=$1">https://scratch.mit.edu/projects/$1</a>').replace(/\n/g, '<br>');
        } catch (error) {
            console.error("Error fetching data:", error);
        }
    }
    
    onMount(async () => {
        getSearchParams();
        if (id) {
            await Promise.all([
                fetchLoves(id),
                fetchStars(id),
                fetchName(id),
                fetchDesc(id)
            ]);
        }
    });
    
    const links = [
      { text: 'Home', url: '/' },
      { text: 'About', url: '/about' },
    ];
</script>
    
<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
  
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background-color: #855CD6;
      color: white;
      font-family: 'Roboto', sans-serif;
      padding: 20px;
    }
  
    .title {
      font-size: 3rem;
      margin-bottom: 20px;
    }
  
    .footer {
      margin-top: 20px;
      font-size: 1rem;
      opacity: 0.7;
    }
  
    .footer a {
      color: white;
      text-decoration: none;
      font-weight: bold;
    }
</style>
    
<Navbar {links} />
<div class="container">
    <h1 class="title">{title}</h1>
    {#if id}
        <iframe src={"https://turbowarp.org/embed/#" + id} title="Project Embed" frameborder="0" allowtransparency="true" allowfullscreen style="width: 100%; min-height: 500px;"></iframe>
        <p>Number of loves: {loves}</p>
        <p>Number of favorites: {favorites}</p>
        <p>{@html desc}</p>
    {:else}
        <p>No ID parameter found.</p>
    {/if}
    <div class="footer">
        Created with ❤️ by <a href="https://github.com/nmsderp" target="_blank">nmsderp</a>
    </div>
</div>
