<template>
  <div id="rectangleComponentContainer">
    
    <toggle-button  v-model="rectangleData.on"
                    color="black"
                    :labels="{checked: 'On', unchecked: 'Off'}"/>
    
    <div id="rectangleComponentTitle">Rectangles</div>
    
    <div id="featureContainer" v-if="rectangleData.on">

      <div class="rectangleFeatureParameters col2">
        <div><span>Quantity: </span><input v-model.number="rectangleData.quantityOfHoles" style="width: 50px" type="number" min="1" step="1"></div>
      </div>

      <div class="col2 row3">Component Title</div>
      <div class="col3 row3">X (in)</div>
      <div class="col4 row3">Angle (deg)</div>
      <div class="col5 row3">Width (in)</div>
      <div class="col6 row3">Height (in)</div>

      <div class="row4 rectangleListSpacing">
        <div v-for="i in rectangleData.quantityOfHoles" :key="i">{{ i }}</div>
      </div>
      <div class="row4 rectangleListSpacing">
        <input v-for="i in rectangleData.quantityOfHoles" :key="i" v-model="rectangleData.componentTitles[i]" type="text">
      </div>
      <div class="row4 rectangleListSpacing">
        <input v-for="i in rectangleData.quantityOfHoles" :key="i" v-model="rectangleData.xCoords[i]" type="number">
      </div>
      <div class="row4 rectangleListSpacing">
        <input v-for="i in rectangleData.quantityOfHoles" :key="i" v-model="rectangleData.angles[i]" type="number">
      </div>
      <div class="row4 rectangleListSpacing">
        <input v-for="i in rectangleData.quantityOfHoles" :key="i" v-model="rectangleData.widths[i]" type="number">
      </div>
      <div class="row4 rectangleListSpacing">
        <input v-for="i in rectangleData.quantityOfHoles" :key="i" v-model="rectangleData.heights[i]" type="number">
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: "RectangleComponent",
  data: function() {
    return {
        rectangleData: {
          on: false,
          quantityOfHoles: 1,
          componentTitles: [],
          xCoords: [],
          angles: [],
          widths: [],
          heights: []
        }
    };
  },
  created() {
      console.log("emitting rectangle data on creation");
      this.$emit('new-data', this.rectangleData);
  },
  watch: {
    rectangleData: {
      handler(val) {
        console.log("rectangle data changed. emitting!");
        this.$emit('new-data', this.rectangleData);
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#rectangleComponentContainer {
  border: solid 1px;
  background-color: #DDADD6;
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

#rectangleComponentTitle {
  grid-column: 1/7;
  font-size: 20px;
  margin-top:-20px;
  text-align: center;
}

.rectangleFeatureParameters {
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

.rectangleListSpacing {
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
