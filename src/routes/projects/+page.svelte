<script>
  import { onMount } from 'svelte';
  import { writable } from 'svelte/store';

  let projects = writable([]);
  let filter = 'all'; // Default filter value
  let isLoading = true;

  const numProjectsToShow = 20;

  async function fetchProjects() {
    try {
      const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/explore/projects?q=${filter}&mode=trending&language=en`);
      const data = await response.json();
      projects.set(data.slice(0, numProjectsToShow));
      isLoading = false;
    } catch (error) {
      console.error('Error fetching projects:', error);
    }
  }

  onMount(fetchProjects);

  async function loadMoreProjects() {
    try {
      const currentProjects = $projects;
      const response = await fetch(`https://corsproxy.io/?https://api.scratch.mit.edu/explore/projects?q=${filter}&mode=trending&language=en&offset=${currentProjects.length}`);
      const newData = await response.json();
      projects.update(existingProjects => [...existingProjects, ...newData.slice(0, numProjectsToShow)]);
    } catch (error) {
      console.error('Error loading more projects:', error);
    }
  }

  function handleProjectClick(projectId) {
    window.location.href = `/view?id=${projectId}`;
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background-color: #855CD6;
    color: white;
    font-family: 'Roboto', sans-serif;
  }

  .title {
    font-size: 3rem;
    margin-bottom: 20px;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    justify-items: center;
    max-width: 1200px;
    width: 100%;
  }

  .project-card {
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 100%;
    max-width: 300px;
    cursor: pointer;
  }

  .project-thumbnail {
    width: 100%;
    border-radius: 10px;
  }

  .project-title {
    margin-top: 10px;
    font-weight: bold;
    font-size: 1.2rem;
    color: black;
  }

  .load-more-button {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #6e4bb3;
    color: white;
    font-size: 1.2rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .load-more-button:hover {
    background-color: #5a3e91;
  }

  .footer {
    margin-top: 50px;
    font-size: 1rem;
    opacity: 0.7;
  }

  .footer a {
    color: white;
    text-decoration: none;
    font-weight: bold;
  }

  .toggle-buttons {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }

  .toggle-buttons button {
    background-color: transparent;
    border: none;
    padding: 10px 20px;
    margin: 0 10px;
    font-size: 1rem;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s;
  }

  .toggle-buttons button:hover {
    background-color: rgba(255, 255, 255, 0.2);
  }

  .toggle-buttons button.active {
    background-color: rgba(255, 255, 255, 0.4);
    color: #855CD6;
  }

  /* New Style for Loading Screen */
  .loading-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .loading-message {
    color: white;
    font-size: 1.5rem;
  }
</style>

<div class="container">
  <div class="title">Explore Projects</div>
  <!-- Toggle Buttons -->
  <div class="toggle-buttons">
    <button class="{filter === 'all' ? 'active' : ''}" on:click={() => { filter = 'all'; fetchProjects(); }}>All</button>
    <button class="{filter === 'games' ? 'active' : ''}" on:click={() => { filter = 'games'; fetchProjects(); }}>Games</button>
    <button class="{filter === 'animations' ? 'active' : ''}" on:click={() => { filter = 'animations'; fetchProjects(); }}>Animations</button>
  </div>

  {#if isLoading}
    <div class="loading-overlay">
      <div class="loading-message">Loading...</div>
    </div>
  {:else}
    <div class="projects-grid">
      {#each $projects as project}
        <div class="project-card" on:click={() => handleProjectClick(project.id)}>
          <img class="project-thumbnail" src={project.image} alt="Project Thumbnail" />
          <div class="project-title">{project.title}</div>
        </div>
      {/each}
    </div>
    <div class="load-more-button" on:click={loadMoreProjects}>Load More</div>
  {/if}

  <div class="footer">
    Created with ❤️ by <a href="https://github.com/nmsderp" target="_blank">nmsderp</a>
  </div>
</div>
