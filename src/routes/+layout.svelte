<script>
    import Navbar from '$lib/components/Navbar.svelte';
  
    const links = [
      { text: 'Home', url: '/' },
      { text: 'About', url: '/about' },
      { text: 'Explore', url: '/projects'}
    ];
  </script>
  
  <Navbar {links} />
  
  <slot />
  