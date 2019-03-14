<template>
  <div id="leftSidebarContainer">
    <div id="leftSidebarTitle">MODIFY COMPONENTS</div>
    <LeftSidebarFeatureButton   v-for="(i) in Object.keys(features).length" 
                                :key="i"
                                :featureType="Object.keys(features)[i-1]"
                                :features="features"/>
  </div>
</template>

<script>
import LeftSidebarFeatureButton from "./LeftSidebarFeatureButton.vue";

export default {
  name: "LeftSidebar",
  props: {
    features: Object
  },
  components: {
    LeftSidebarFeatureButton
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#leftSidebarContainer {
  display: grid;
  gap: 10px;
  grid-auto-rows: min-content;
}

#leftSidebarTitle {
  font-size: 12px;
}
</style>
