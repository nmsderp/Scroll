<script>
    import Navbar from '$lib/components/Navbar.svelte';
  
    function exploreProjects() {
      window.location.href = '/projects';
    }
  
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
      height: 100vh;
      background-color: #855CD6;
      color: white;
      font-family: 'Roboto', sans-serif;
    }
  
    .title {
      font-size: 3rem;
      margin-bottom: 20px;
    }
  
    .button {
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      background-color: #6e4bb3;
      color: white;
      font-size: 1.5rem;
      cursor: pointer;
      transition: background-color 0.3s;
    }
  
    .button:hover {
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
  </style>
    
  <Navbar {links} />
  <div class="container">
    <h1 class="title">Welcome to Scroll!</h1>
    <p>A faster Scratch frontend.</p>
    <button class="button" on:click={exploreProjects}>Explore Projects</button>
    <div class="footer">
      Created with ❤️ by <a href="https://github.com/nmsderp" target="_blank">nmsderp</a>
    </div>
  </div>
  