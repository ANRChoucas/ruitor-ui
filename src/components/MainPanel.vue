<template>
<div id="mainPanelGrid">
  <div id="spatialisationPanel" class="panel">
    <div class="titleBox panelBox">
      <span>xxxxx</span>
      <span>yyyy</span>
      <button v-on:click="test.push(100)">+</button>
    </div>
    <div v-if="test">
      <div v-for="i in test" v-bind:key="i" class="panelBox">
        <span>{{ i }}</span> <span>{{ i * 2}}</span>
      </div>
    </div>
  </div>
  <div id="fusionPanel" class="panel">
    <div class="titleBox panelBox">
      <span>xxxxx</span>
      <span>yyyy</span>
      <button v-on:click="fus.push(20)">+</button>
    </div>
    <div v-if="fus">
      <div v-for="i in fus" v-bind:key="i" class="panelBox">
        <span>{{ i }}</span> <span>{{ i * 2}}</span>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
    data()
    {
        return {
            test: [],
            fus: [],
        }
    }
    
}
</script>

<style scoped>
  #mainPanelGrid {
  height: 100%;
  
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: max-content 1fr;

  
  }
  
  .panel{
  border: solid;
  grid-column: 1;

  overflow: auto;
  }
  
  
  #spatialisationPanel{
  grid-row:1;

  height: 60vh;
  resize: vertical;
  
  }
  
  #fusionPanel{
  grid-row:2;
  }

  .panelBox{
  display: flex;
  justify-content: space-between;
  

  border: dashed;
  }

  .titleBox{
  height:25px;
  
  }
</style>
