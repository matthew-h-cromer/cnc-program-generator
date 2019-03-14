<template>
  <div class='container'>
    <div class = 'title'>Part Information</div>
    <div class = 'parameter'>Part Number</div><div class='inputContainer'><input type='text'></div>            <div class = 'parameter'>Revision</div><div class='inputContainer'><input type='text'></div>
    <div class = 'parameter'>Date</div><div class='inputContainer'><input type='text'></div>                   <div class = 'parameter'>Shell Diameter</div><div class='inputContainer'><input type='text'></div>
    <div class = 'parameter'>Created by</div><div class='inputContainer'><input type='number'></div>           <div class = 'parameter'></div><div class='inputContainer'></div>
    <div class='status'>Status</div>
  </div>
</template>

<script>
export default {
  name: 'ShellInformation',
  props: {
    titleMessage: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

input {
    padding:5px; 
    border:2px solid gray; 
    -webkit-border-radius: 5px;
    border-radius: 5px;
}

.title {
    grid-column: 1/5;
    padding: 5px 0 5px 0;
    font-size: 20px;
}

.container {
    display: grid;
    grid-column: 1/3;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-flow: row;
    text-align: center;
    border: solid 1px;
    background-color:lightgray;
    -webkit-border-radius: 5px;
    border-radius: 5px;
    grid-row-gap: 2px;
    width: 2fr;
}

.parameter {
    padding: 5px;
}

.status {
    grid-column: 1/5;
    padding: 5px;
}

.inputContainer {
    padding: 0 10px 0 0;
}
</style>
