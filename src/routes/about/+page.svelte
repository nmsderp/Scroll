<script>
  import { goto } from "$app/navigation";
  
    function exploreProjects() {
      goto('/projects');
    }
  
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
    .github-link {
        color: #000000; /* Dark blue color */
        text-decoration: none; /* Remove underline */
    }

    .github-link:hover {
        text-decoration: underline; /* Underline on hover */
    }
  </style>
    
  <div class="container">
    <h1 class="title">About Scroll</h1>
    <p>Scroll is a simple Scratch frontend that runs projects via TurboWarp.</p>
    <h1 class="title">What is a Frontend?</h1>
    <p>A frontend is a website or piece of software that interacts with a server to show data.</p>
    <h1 class="title">Can I Contribute?</h1>
    <p>Yes! You can also contribute to us via our <a href="https://github.com/nmsderp/Scroll" class="github-link">GitHub repo</a></p>

    <button class="button" on:click={exploreProjects}>Explore Projects</button>
    <div class="footer">
      Created with ❤️ by <a href="https://github.com/nmsderp" target="_blank">nmsderp</a>
    </div>
  </div>
  