<template>
  <div id="holeComponentContainer">
    <div id="holeComponentTitle">Shell Parameters</div>

    <div class="holeFeatureParameters">
      <div><span>Part Number: </span><input v-model="shellParametersData.partNumber" type="text"></div>
      <div><span>Revision: </span><input v-model="shellParametersData.revision" type="text"></div>
      <div><span>Created by: </span><input v-model="shellParametersData.createdBy" type="text"></div>
    </div>

    <div class="holeFeatureParameters">
      <div><span>Shell Diameter: </span><input v-model="shellParametersData.shellDiameter" type="number" min="0" step="0.5"></div>
    </div>

  </div>
</template>

<script>
export default {
  name: "ShellParametersComponent",
  data: function() {
    return {
        shellParametersData: {
          shellDiameter: 0,
          partNumber: "",
          revision: "",
          createdBy: ""
        }
    };
  },
  created() {
      console.log("emitting shell data on creation");
      this.$emit('new-data', this.shellParametersData);
  },
  watch: {
    shellParametersData: {
      handler(val) {
        console.log("shell data changed. emitting!");
        this.$emit('new-data', this.shellParametersData);
      },
      deep: true
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#holeComponentContainer {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  border: solid 1px;
  background-color: #EDE3E4;
  -webkit-border-radius: 3px;
  border-radius: 3px;
  padding: 5px;
  justify-items: center;
  align-items:start;
  align-content: center;
  text-align: center;
  gap: 10px;
  margin-bottom: 10px;
}

#holeComponentTitle {
  grid-column: 1/3;
  font-size: 20px;
  margin-bottom: 15px;
}

.holeFeatureParameters {
  display: grid;
  justify-items: right;
  gap: 4px;

  background:#E7DFE8;

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
  margin-top: 15px;
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
}

</style>
