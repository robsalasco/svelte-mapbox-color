<script>
  import Mapbox from "./Mapbox.svelte";
  import Layout from './Layout.svelte';
  import ColorChanger from "./ColorChanger.svelte";

  // https://stackoverflow.com/questions/1484506/random-color-generator
  function getRandomColor() {
    var letters = '0123456789ABCDEF';
    var color = '#';
    for (var i = 0; i < 6; i++) {
      color += letters[Math.floor(Math.random() * 16)];
    }
    return color;
  }

  let mapComponent; 
  let selected = "#bd0026";
  let mounted = true;

  function randomColor() {
    selected = getRandomColor();
  }

  $: { reMountMap( selected ) }
  
  function reMountMap(){
    mounted = false;
    setTimeout(() => mounted = true, 0);
  }

</script>

<Layout>
  <span slot="left">
  <button on:click={mapComponent.flyTo()}>Fly</button>
  <button on:click={randomColor}>Random road color</button>

  </span>
  <span slot="right">
      <Mapbox bind:this={mapComponent}>
      {#if mounted}
      <ColorChanger roadcolor={selected} />
      {/if}
      </Mapbox>
  </span>
</Layout>
