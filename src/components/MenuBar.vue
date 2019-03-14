<template>
  <div id="menuBarContainer">
    <div class="button" v-on:click='showReference = !showReference'>Toggle Reference</div>
    <div class="button settings">Settings</div>
    <div @click="$emit('generate-button-clicked')" class="button generate">Generate G-Code</div>
    <img id="reference" src="ShellDiagram.png" v-show="showReference">
  </div>
</template>

<script>
export default {
  name: "MenuBar",
  props: {
    programArray: Array
  },
  data: function () {
    return {
      textFile: Object,
      showReference: false
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  padding: 5px;
  border: 2px solid #ccc;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}

#reference {
  grid-column: 1/4;
  width: 100%;
}

.title {
  grid-column: 1/3;
  padding: 5px 0 5px 0;
  font-size: 20px;
}

#menuBarContainer {
  grid-column: 1/3;
  display: grid;
  justify-items: center;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-flow: row;
  grid-gap: 20px;
  margin-bottom: 20px;
}

.parameter {
  padding: 5px;
}

.status {
  grid-column: 1/3;
  padding: 5px;
}

.button {
    border: 2px solid black;
    background-color: darkslategrey;
    color:white;
    -webkit-border-radius: 5px;
    border-radius: 5px;
    width: 200px;
}

.generate {
  background-color: rgb(11, 168, 108);
}

.settings {
 background-color: gray;
 color: lightgray;
}

</style>
