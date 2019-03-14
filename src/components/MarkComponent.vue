<template>
  <div id="holeComponentContainer">
    
    <toggle-button  v-model="markData.on"
                    color="black"
                    :labels="{checked: 'On', unchecked: 'Off'}"/>
    
    <div id="holeComponentTitle">Marks</div>

    <div id="featureContainer" v-if="markData.on">

      <div class="holeFeatureParameters col2">
        <div><span>Quantity: </span><input v-model.number="markData.quantityOfMarks" style="width: 50px" type="number" min="1" step="1"></div>
      </div>

      <div class="col2 row3">Component Title</div>
      <div class="col3 row3">X (in)</div>
      <div class="col4 row3">Y (in)</div>
      <div class="col5 row3">Angle (deg)</div>

      <div class="row4 holeListSpacing">
        <div v-for="i in markData.quantityOfMarks" :key="i">{{ i }}</div>
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in markData.quantityOfMarks" :key="i" v-model="markData.componentTitles[i]" type="text">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in markData.quantityOfMarks" :key="i" v-model="markData.xCoords[i]" type="number">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in markData.quantityOfMarks" :key="i" v-model="markData.yCoords[i]" type="number">
      </div>
      <div class="row4 holeListSpacing">
        <input v-for="i in markData.quantityOfMarks" :key="i" v-model="markData.angles[i]" type="number">
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "MarkComponent",
  data: function() {
    return {
        markData: {
          on: false,
          quantityOfMarks: 1,
          componentTitles: [],
          xCoords: [],
          yCoords: [],
          angles: []
        }
    };
  },
  created() {
      console.log("emitting mark data on creation");
      this.$emit('new-data', this.markData);
  },
  watch: {
    markData: {
      handler(val) {
        console.log("mark data changed. emitting!");
        this.$emit('new-data', this.markData);
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
  background-color: #9AD1D4;
  -webkit-border-radius: 3px;
  border-radius: 3px;
  padding: 5px;
  text-align: left;
  align-items:start;
  align-content: center;
  margin-bottom: 10px;
}

#featureContainer {
  display: grid;
  grid-template-columns: 50px repeat(5, 1fr);
  text-align: center;
  gap: 10px;
}

#holeComponentTitle {
  grid-column: 1/7;
  font-size: 20px;
  margin-top: -20px;
  text-align: center;
}

.holeFeatureParameters {
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
