<script>
  import Mapbox from "./Mapbox.svelte";
  import Layout from './Layout.svelte';
  import ColorChanger from "./ColorChanger.svelte";
  import ChromaPicker from 'svelte-chroma-picker';


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
  let selected;
  let mounted = true;
  let rgb

  function randomColor() {
    selected = getRandomColor();
  }

  const handleColorUpdate = ev => {
    rgb = ev.detail.rgb;

    let r = rgb.r;
    let g = rgb.g;
    let b = rgb.b;

    selected = `rgb(${r},${g},${b})`;
  };

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
  <ChromaPicker bind:selected  on:update={handleColorUpdate} />
  </span>
  <span slot="right">
      <Mapbox bind:this={mapComponent}>
      {#if mounted}
      <ColorChanger roadcolor={selected} />
      {/if}
      </Mapbox>
  </span>
</Layout>
