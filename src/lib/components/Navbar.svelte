<script>
  import { goto } from "$app/navigation";
  export let links = [];
  
  function navigateTo(url) {
    goto(url); 
  }
</script>

<nav>
  <ul>
    {#each links as link}
      <li>
        <a href={link.url} on:click|preventDefault={() => navigateTo(link.url)}>
          {link.text}
        </a>
      </li>
    {/each}
  </ul>
</nav>

<style>
  :global(nav) {
    background-color: #333;
    color: white;
    padding: 1rem;
    font-family: 'Roboto', sans-serif;
  }

  :global(ul) {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: space-between;
  }

  :global(li) {
    margin: 0 1rem;
  }

  :global(a) {
    color: white;
    text-decoration: none;
    transition: opacity 0.2s;
  }

  :global(a:hover) {
    opacity: 0.8;
  }
</style>
