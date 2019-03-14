<template>
  <div id="surgeSlotComponentContainer">
    
    <toggle-button  v-model="surgeSlotData.on"
                    color="black"
                    :labels="{checked: 'On', unchecked: 'Off'}"/>
    
    <div id="surgeSlotComponentTitle">Surge Tank Slot {{ surgeSlotData.surgeSlotID }}</div>
  
    <div id="featureContainer" v-if="surgeSlotData.on">

      <div class="col1 row2">Shell Length (in)</div>
      <div class="col2 row2">Shell-to-shell Offset (in)</div>
      <div class="col3 row2">Mating Shell Diameter (in)</div>

      <div class="col1 row3 surgeSlotListSpacing">
        <input v-model="surgeSlotData.shellLength" type="text">
      </div>
      <div class="col2 row3 surgeSlotListSpacing">
        <input v-model="surgeSlotData.shellToShellOffset" type="number">
      </div>
      <div class="col3 row3 surgeSlotListSpacing">
        <input v-model="surgeSlotData.matingShellDiameter" type="number">
      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: "SurgeSlotComponent",
  data: function() {
    return {
        surgeSlotData: {
          on: false,
          shellLength: 0,
          shellToShellOffset: 0,
          matingShellDiameter: 0
        }
    };
  },
  created() {
      console.log("emitting surge tank slot data on creation");
      this.$emit('new-data', this.surgeSlotData);
  },
  watch: {
    surgeSlotData: {
      handler(val) {
        console.log("surge tank slot data changed. emitting!");
        this.$emit('new-data', this.surgeSlotData);
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#surgeSlotComponentContainer {
  
  border: solid 1px;
  background-color: #95A3B3;
  -webkit-border-radius: 3px;
  border-radius: 3px;
  padding: 5px;
  justify-items: center;
  align-items:start;
  align-content: center;
  margin-bottom: 10px;
  text-align: left;
}

#featureContainer {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  text-align: center;
  gap: 10px;
}

#surgeSlotComponentTitle {
  grid-column: 1/4;
  font-size: 20px;
  text-align: center;
  margin-top: -20px;
}

.surgeSlotFeatureParameters {
  display: grid;
  justify-items: right;
  gap: 4px;

  background: #E7DFE8;

  padding: 4px;
  margin: 8px auto;

  border: 1px solid black;
  -webkit-border-radius: 3px;
  border-radius: 3px;
}

.col1 {
  grid-column: 1;
}

.col2 {
  grid-column: 2;
}

.col3-4 {
  grid-column: 3/5;
}

.col3 {
  grid-column: 3;
}

.col4 {
  grid-column: 4;
}

.col5-6 {
  grid-column: 5/7
}

.col5 {
  grid-column: 5;
}

.col6 {
  grid-column: 6;
}

.row2 {
  grid-row: 2;
  margin-top: 15px;
}

.row3 {
  grid-row: 3;
}

.surgeSlotListSpacing {
  display: inline-grid;
  grid-auto-rows: 30px;
  align-items: center;
  justify-items: center;
}

input {
  border: 2px solid gray;
  -webkit-border-radius: 5px;
  border-radius: 5px;
  text-align: center;
}

</style>
