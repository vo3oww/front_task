<template>
  <div>
    <b-button block :variant="variant" :type="type">{{text}}</b-button>
  </div>
</template>

<script>
export default {
  props :{
    variant : {
      type : String
    },
    text : {
      type : String
    },
    type : {
      type : String
    }
  },
};
</script>