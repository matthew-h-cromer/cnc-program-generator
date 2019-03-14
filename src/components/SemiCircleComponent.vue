<template>
  <div id="semiCircleComponentContainer">
    
    <toggle-button  v-model="semiCircleData.on"
                    color="black"
                    :labels="{checked: 'On', unchecked: 'Off'}"/>
    
    <div id="semiCircleComponentTitle">Semi Circles</div>
    
    <div id="featureContainer" v-if="semiCircleData.on">

      <div class="semiCircleFeatureParameters col2">
        <div><span>Quantity: </span><input v-model.number="semiCircleData.quantityOfHoles" style="width: 50px" type="number" min="1" step="1"></div>
      </div>

      <div class="col2 row3">Component Title</div>
      <div class="col3 row3">Hole Diameter (in)</div>
      <div class="col4 row3">X (in)</div>
      <div class="col5 row3">Angle (deg)</div>
      <div class="col6 row3">Left/Right Facing</div>

      <div class="row4 semiCircleListSpacing">
        <div v-for="i in semiCircleData.quantityOfHoles" :key="i">{{ i }}</div>
      </div>
      <div class="row4 semiCircleListSpacing">
        <input v-for="i in semiCircleData.quantityOfHoles" :key="i" v-model="semiCircleData.componentTitles[i]" type="text">
      </div>
      <div class="row4 semiCircleListSpacing">
        <input v-for="i in semiCircleData.quantityOfHoles" :key="i" v-model="semiCircleData.semiCircleDiameters[i]" type="number">
      </div>
      <div class="row4 semiCircleListSpacing">
        <input v-for="i in semiCircleData.quantityOfHoles" :key="i" v-model="semiCircleData.xCoords[i]" type="number">
      </div>
      <div class="row4 semiCircleListSpacing">
        <input v-for="i in semiCircleData.quantityOfHoles" :key="i" v-model="semiCircleData.angles[i]" type="number">
      </div>
      <div class="row4 semiCircleListSpacing">
        <toggle-button v-for="i in semiCircleData.quantityOfHoles" :key="i" 
               v-model="semiCircleData.leftRight[i]" 
               :color="{checked: 'grey', unchecked: 'grey'}"
               :width="toggleButtonWidth"
               :labels="{checked: 'Right', unchecked: 'Left'}"/>
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: "SemiCircleComponent",
  data: function() {
    return {
        toggleButtonWidth: 80,
        semiCircleData: {
          on: false,
          quantityOfHoles: 1,
          componentTitles: [],
          semiCircleDiameters: [],
          xCoords: [],
          angles: [],
          leftRight: [false]
        }
    };
  },
  created() {
      console.log("emitting semiCircle data on creation");
      this.$emit('new-data', this.semiCircleData);
  },
  watch: {
    semiCircleData: {
      handler(val) {
        console.log("semiCircle data changed. emitting!");
        this.$emit('new-data', this.semiCircleData);
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#semiCircleComponentContainer {
  border: solid 1px;
  background-color: #E3D985;
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

#semiCircleComponentTitle {
  grid-column: 1/7;
  font-size: 20px;
  margin-top:-20px;
  text-align: center;
}

.semiCircleFeatureParameters {
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

.semiCircleListSpacing {
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
