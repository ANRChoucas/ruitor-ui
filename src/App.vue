<template>
  <div id="body_grid">
    <header>
      <h1>Ruitor UI</h1>
    </header>
<div id="grid">
  <div id="map">
    <Map/>
  </div>
  <div id="mainpanel">
    <MainPanel/>
  </div>
</div>
</div>
</template>

<script>
import Map from './components/Map.vue'
import MainPanel from './components/MainPanel.vue'


export default {
    name: 'App',
    components: {
        MainPanel,
        Map
    }
}
</script>

<style>

:root {
  --nord0: #2e3440;
  --nord1: #3b4252;
  --nord2: #434c5e;
  --nord3: #4c566a;
  --nord4: #d8dee9;
  --nord5: #e5e9f0;
  --nord6: #eceff4;
  --nord7: #8fbcbb;
  --nord8: #88c0d0;
  --nord9: #81a1c1;
  --nord10: #5e81ac;
  --nord11: #bf616a;
  --nord12: #d08770;
  --nord13: #ebcb8b;
  --nord14: #a3be8c;
  --nord15: #b48ead;
}

  
body{
    width: 100vw;
    height: 100vh;
    
    margin: 0;
    overflow: hidden;

    background-color: var(--nord0);
    color: var(--nord4);
    
}

header {
    height: 50px;
    background: var(--nord0);

    display: flex;
    align-items: center;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    
    width: inherit;
    height: inherit;
}

#body_grid {
    display: grid;

    grid-template-columns: 1fr;
    grid-template-rows: min-content 1fr;
    
    width: inherit;
    height: inherit;
}

#grid {
    display: grid;
    
    grid-auto-columns: 1fr;
    grid-template-columns: max-content 1fr;
    grid-template-rows: auto;
    grid-gap:10px;
}


#map{  
    grid-column-start: 1;
    grid-column-end: auto;
    grid-row-start: 1;
    grid-row-end: auto;

    width: 75vw;
    
    resize: horizontal;
    overflow:auto;

    background: var(--nord3);
}

#mainpanel {
    grid-column-start: 2;
    grid-column-end: auto;
    grid-row-start: 1;
    grid-row-end: auto;

    background: var(--nord3);
}

h1 {
    color: var(--nord4);

}
</style>
