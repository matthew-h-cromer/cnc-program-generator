<template>
  <div id="app">

    <!-- TOP SIDEBAR -->
    <a class="button" href="http://www.matthewcromer.me">Back to portfolio</a>
    <div id="topContainer">
      <span id="appTitle">Shell Program Generator</span>
    </div>

    <!-- INTRO PAGE -->

    <!-- CENTER CONTAINER -->
    <div id="centerContainer">
      <MenuBar  @generate-button-clicked="generate()"/>
      <!-- slot to display settings or toggle reference -->
      <ShellParametersComponent  @new-data="saveShellParametersData($event)"/>
      <HoleComponent  @new-data="saveHoleData($event)"/>
      <MarkComponent  @new-data="saveMarkData($event)"/>
      <SurgeSlotComponent  @new-data="saveSurgeSlotData($event)"/>
      <SemiCircleComponent  @new-data="saveSemiCircleData($event)"/>
      <RectangleComponent  @new-data="saveRectangleData($event)"/>
    </div>

  </div>
</template>

<script>
import ShellParametersComponent from "./components/ShellParametersComponent.vue";
import HoleComponent from "./components/HoleComponent.vue";
import SemiCircleComponent from "./components/SemiCircleComponent.vue"
import RectangleComponent from "./components/RectangleComponent.vue"
import MarkComponent from "./components/MarkComponent.vue";
import SurgeSlotComponent from "./components/SurgeSlotComponent.vue";
import MenuBar from "./components/MenuBar.vue";
import ShellTemplate from 'raw-loader!./assets/Shell Program Template.txt';

export default {
  name: "app",
  components: {
    ShellParametersComponent,
    HoleComponent,
    SemiCircleComponent,
    RectangleComponent,
    MarkComponent,
    SurgeSlotComponent,
    MenuBar
  },
  data: function() {
    return {
      featureData: {  shellParametersData: Object,
                      holeData: Object,
                      surgeSlotData: Object
      },
      switch1: true
    };
  },
  methods: {
    generate: function () {
      //GENERATE CODE
      var text = this.buildProgramCode();

      //DOWNLOAD CODE
      this.downloadTextFile(text);
    },
    downloadTextFile: function (text) {
      var filename = this.featureData.shellParametersData.partNumber + "-REV" + this.featureData.shellParametersData.revision +".txt";
      var element = document.createElement('a');
      
      element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
      element.setAttribute('download', filename);

      element.style.display = 'none';
      document.body.appendChild(element);

      element.click();

      document.body.removeChild(element);
    },
    buildProgramCode: function () {
      var i;
      var text = ShellTemplate;
      var date = new Date();
      var insert = "";

      //Replace variables by *tag*:
        text = text.replace("*partNumber*", this.featureData.shellParametersData.partNumber);
        text = text.replace("*revision*", this.featureData.shellParametersData.revision);
        text = text.replace("*createdBy*", this.featureData.shellParametersData.createdBy);
        text = text.replace("*shellDiameter*", this.featureData.shellParametersData.shellDiameter);
        text = text.replace("*date*", date);

      //  *markSubroutineCall*
      if (this.featureData.markData.on) {
        insert = "";
        for (i = 1; i <= this.featureData.markData.quantityOfMarks; i++) { 
          insert += "(MARK " + i + ")" + "\r\n";
          insert += "(Component: " + this.featureData.markData.componentTitles[i] + ")" + "\r\n";
          insert += "#11= " + this.featureData.markData.xCoords[i] + " (X Distance to hole center)" + "\r\n";
          insert += "#12= " + this.featureData.markData.yCoords[i] + " (Y Distance to hole center)" + "\r\n";
          insert += "#13= " + this.featureData.markData.angles[i] + " (Angle from Y plane)" + "\r\n";
          insert += "M97 P1001 (MARK SUBROUTINE)" + "\r\n" + "\r\n";
        }
        text = text.replace("*markSubroutineCall*", insert + "\r\n" + "\r\n");   
      } else {
        text = text.replace("*markSubroutineCall*", "");
      }

      //  *holeSubroutineCall*
      if (this.featureData.holeData.on) {
        insert = "";
        for (i = 1; i <= this.featureData.holeData.quantityOfHoles; i++) { 
          insert += "(HOLE " + i + ")" + "\r\n";
          insert += "(Component: " + this.featureData.holeData.componentTitles[i] + ")" + "\r\n";
          insert += "#17= " + this.featureData.holeData.xCoords[i] + " (X Distance to hole center)" + "\r\n";
          insert += "#18= " + this.featureData.holeData.yCoords[i] + " (Y Distance to hole center)" + "\r\n";
          insert += "#19= " + this.featureData.holeData.angles[i] + " (Angle from Y plane)" + "\r\n";
          insert += "#20= " + this.featureData.holeData.holeDiameters[i] + " (Hole diameter)" + "\r\n";
          insert += "M97 P1002 (HOLE SUBROUTINE)" + "\r\n" + "\r\n";
        }
        text = text.replace("*holeSubroutineCall*", insert + "\r\n" + "\r\n");
      } else {
        text = text.replace("*holeSubroutineCall*", "");
      }
      
      //  *surgeTankChannelSubroutineCall*
      if (this.featureData.surgeSlotData.on) {
        insert = "";
        insert += "(SURGE TANK SLOT)" + "\r\n";
        insert += "#14= " + this.featureData.surgeSlotData.shellLength + " (Shell Length)" + "\r\n";
        insert += "#15= " + this.featureData.surgeSlotData.shellToShellOffset + " (Shell-shell Offset)" + "\r\n";
        insert += "#16= " + this.featureData.surgeSlotData.matingShellDiameter + " (Mating Shell Diameter 2, 2.5, 3, 4, 5, 6)" + "\r\n";
        insert += "M97 P1003 (SURGE SLOT SUBROUTINE)" + "\r\n";
        text = text.replace("*surgeTankChannelSubroutineCall*", insert + "\r\n" + "\r\n");
      } else {
        text = text.replace("*surgeTankChannelSubroutineCall*", "");
      }

      //  *semiCircleSubroutineCall*
      var leftRight = null; //Conversion --> {Right->TRUE->1}  {Left->FALSE->0} 
      
      if (this.featureData.semiCircleData.on) {
        insert = "";
        
        for (i = 1; i <= this.featureData.semiCircleData.quantityOfHoles; i++) {
          if (this.featureData.semiCircleData.leftRight[i]) { //semiCircleData.leftRight is TRUE when RIGHT
            leftRight = 1; //RIGHT
          } else {
            leftRight = 0; //LEFT
          } 

          insert += "(SEMI CIRCLE " + i + ")" + "\r\n";
          insert += "(Component: " + this.featureData.semiCircleData.componentTitles[i] + ")" + "\r\n";
          insert += "#25= " + this.featureData.semiCircleData.xCoords[i] + " (X distance to hole center)" + "\r\n";
          insert += "#26= " + this.featureData.semiCircleData.angles[i] + " (Angle from Y plane)" + "\r\n";
          insert += "#27= " + this.featureData.semiCircleData.semiCircleDiameters[i] + " (Semi Circle Diameter)" + "\r\n";
          insert += "#28= " + leftRight + " (Pointing Left{0}/Right{1})" + "\r\n";
          insert += "M97 P1005 (SEMI CIRCLE SUBROUTINE)" + "\r\n" + "\r\n";
        }
        text = text.replace("*semiCircleSubroutineCall*", insert + "\r\n" + "\r\n");
      } else {
        text = text.replace("*semiCircleSubroutineCall*", "");
      }

      //  *rectangleSubroutineCall*
      if (this.featureData.rectangleData.on) {
        insert = "";
        for (i = 1; i <= this.featureData.rectangleData.quantityOfHoles; i++) { 
          insert += "(RECTANGLE " + i + ")" + "\r\n";
          insert += "(Component: " + this.featureData.rectangleData.componentTitles[i] + ")" + "\r\n";
          insert += "#30= " + this.featureData.rectangleData.xCoords[i] + " (X Distance to hole center)" + "\r\n";
          insert += "#31= " + this.featureData.rectangleData.angles[i] + " (Angle from Y plane)" + "\r\n";
          insert += "#32= " + this.featureData.rectangleData.widths[i] + " (Width)" + "\r\n";
          insert += "#33= " + this.featureData.rectangleData.heights[i] + " (Height)" + "\r\n";
          insert += "M97 P1006 (RECTANGLE SUBROUTINE)" + "\r\n" + "\r\n";
        }
        text = text.replace("*rectangleSubroutineCall*", insert + "\r\n" + "\r\n");
      } else {
        text = text.replace("*rectangleSubroutineCall*", "");
      }


/*       (RECTANGLE 1)
      #30 = 0 (X distance to rectangle center)
      #31 = 0 (angle from Y plane)
      #32 = 0 (rectangle width)
      #33 = 0 (rectangle height)
      M97 P1006 */


      return text;
    },
    saveHoleData (holeData) {
      this.featureData.holeData = holeData;
    },
    saveMarkData: function (markData) {
      this.featureData.markData = markData;
    },
    saveSurgeSlotData: function (surgeSlotData) {
      this.featureData.surgeSlotData = surgeSlotData;
    },
    saveShellParametersData: function (shellParametersData) {
      this.featureData.shellParametersData = shellParametersData;
    },
    saveSemiCircleData: function (semiCircleData) {
      this.featureData.semiCircleData = semiCircleData;
    },
    saveRectangleData: function (rectangleData) {
      this.featureData.rectangleData = rectangleData;
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400");

#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  justify-items: center;
  display: grid;
  grid-template-columns: 1fr 5fr 1fr;
  grid-gap: 10px;
  grid-auto-flow: row;
  width: 1200px;
  margin: 0 auto;
}

#topContainer {
  display: grid;
  grid-column: 1/4;
}

#leftContainer {
  display: inline-grid;
  border: solid;
  -webkit-border-radius: 5px;
  border-radius: 5px;
  padding: 5px;
}

#rightContainer {
  display: inline-grid;
  border: solid;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}

#centerContainer {
  border: solid;
  grid-column: 2;
  -webkit-border-radius: 5px;
  border-radius: 5px;
  padding: 5px;
}

#appTitle {
  grid-column: 1/3;
  font-weight: 300;
  font-size: 30px;
  padding-bottom: 20px;
  color: black;
}

.button {
    border: 2px solid lightgray;
    background-color:#162521;
    color:whitesmoke;
    -webkit-border-radius: 5px;
    border-radius: 5px;
    text-decoration: none;
}

</style>
