<template>
  <div id="holeComponentContainer">
    
    <toggle-button  v-model="holeData.on"
                    color="black"
                    :labels="{checked: 'On', unchecked: 'Off'}"/>
    
    <div id="holeComponentTitle">Holes</div>
    
    <div id="featureContainer" v-if="holeData.on">

      <div class="holeFeatureParameters col2">
        <div><span>Quantity: </span><input v-model.number="holeData.quantityOfHoles" style="width: 50px" type="number" min="1" step="1"></div>
      </div>

      <div class="col2 row3">Component Title</div>
      <div class="col3 row3">Hole Diameter (in)</div>
      <div class="col4 row3">X (in)</div>
      <div class="col5 row3">Y (in)</div>
      <div class="col6 row3">Angle (deg)</div>

      <div class="row4 holeListSpacing">
        <div v-for="i in holeData.quantityOfHoles" :key="i">{{ i }}</div>
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in holeData.quantityOfHoles" :key="i" v-model="holeData.componentTitles[i]" type="text">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in holeData.quantityOfHoles" :key="i" v-model="holeData.holeDiameters[i]" type="number">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in holeData.quantityOfHoles" :key="i" v-model="holeData.xCoords[i]" type="number">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in holeData.quantityOfHoles" :key="i" v-model="holeData.yCoords[i]" type="number">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in holeData.quantityOfHoles" :key="i" v-model="holeData.angles[i]" type="number">
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: "HoleComponent",
  data: function() {
    return {
        holeData: {
          on: false,
          quantityOfHoles: 1,
          componentTitles: [],
          holeDiameters: [],
          xCoords: [],
          yCoords: [],
          angles: []
        }
    };
  },
  created() {
      console.log("emitting hole data on creation");
      this.$emit('new-data', this.holeData);
  },
  watch: {
    holeData: {
      handler(val) {
        console.log("hole data changed. emitting!");
        this.$emit('new-data', this.holeData);
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#holeComponentContainer {
  border: solid 1px;
  background-color: #86E7B8;
  -webkit-border-radius: 3px;
  border-radius: 3px;
  padding: 5px;
  justify-items: left;
  align-items:start;
  align-content: left;
  text-align: left;
  margin-bottom: 10px;
  width: 857px;
}

#featureContainer {
  display: grid;
  grid-template-columns: 50px repeat(5, 1fr);
  gap: 10px;
  text-align: center;
}

#holeComponentTitle {
  grid-column: 1/7;
  font-size: 20px;
  margin-top:-20px;
  text-align: center;
}

.holeFeatureParameters {
  display: grid;
  justify-items: right;
  gap: 4px;

  background: #E7DFE8;

  padding: 4px;
  margin-top: 6px;
  margin-bottom: 6px;

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

.row3 {
  grid-row: 3;
}

.row4 {
  grid-row: 4;
}

.holeListSpacing {
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
  width: 100%;
}

</style>
