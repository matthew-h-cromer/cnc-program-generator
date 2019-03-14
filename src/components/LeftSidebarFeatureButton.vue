<template>
    <div id="featureButtonContainer">
        <div id="featureButtonTitle">{{ featureType }}</div>
        <input v-model="features[featureType].quantity">
        <button @click="features[featureType].quantity--">-</button>
        <button @click="features[featureType].quantity++">+</button>
    </div>
</template>

<script>
export default {
    name: "LeftSidebarFeatureButton",
    props: {
        featureType: String,
        features: Object
    },
    data: function () {
        return {
            test: 0
        }
    }
};
</script>

<style>
#featureButtonContainer {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    gap: 3px;
}

#featureButtonTitle {
    border: 1px solid;
    background-color:rgba(61, 191, 214, 0.767);
    -webkit-border-radius: 5px;
    border-radius: 5px;
    grid-column: 1/4;
    padding: 2px;
    font-size: 16px;
}

input {
    border: 1px solid;
    -webkit-border-radius: 5px;
    border-radius: 5px;
    width: 90%;
    text-align: center;
}

button{
    border: 1px solid;
    -webkit-border-radius: 5px;
    border-radius: 5px;
}

</style>