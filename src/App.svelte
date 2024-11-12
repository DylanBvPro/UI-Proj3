<script>
  import { onMount } from 'svelte';
  import svelteLogo from './assets/svelte.svg';
  import viteLogo from '/vite.svg';
  import Counter from './lib/Counter.svelte';

  // Replace with your own Google Maps API key
  const apiKey = 'AIzaSyCfADU3lbR7Z_8wUdPrzzXwV3cHEIFRKww';

  let map;
  const mapOptions = {
    center: { lat: 40.12150192260742, lng: -100.45039367675781 },
    zoom: 4,
  };

  onMount(() => {
    // Dynamically load the Google Maps API
    const script = document.createElement('script');
    script.src = `https://maps.googleapis.com/maps/api/js?key=${apiKey}&callback=initMap&libraries=maps,marker&v=beta`;
    script.async = true;
    window.initMap = () => {
      // Initialize map once the API is loaded
      map = new google.maps.Map(document.getElementById('map'), mapOptions);

      // Add a marker
      new google.maps.Marker({
        position: mapOptions.center,
        map: map,
        title: 'My location',
      });
    };
    document.head.appendChild(script);
  });
</script>

<main>
  <!-- Vite and Svelte logos -->
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <!-- Counter component -->
  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>

  <!-- Google Map container -->
  <div id="map"></div>
</main>

<style>
  /* Vite and Svelte logos styling */
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }

  /* Map styling */
  #map {
    width: 100%;
    height: 500px; /* Set the desired height for the map */
    margin-top: 2em;
  }
</style>
