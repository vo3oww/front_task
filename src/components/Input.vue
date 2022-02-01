<template>
  <b-container fluid style="text-align: left">
    <b-row class="my-1">
      <b-col sm="3">
        <label>{{ title }}</label>
      </b-col>
    </b-row>
    <b-row class="my-1">
      <b-col sm="9">
        <b-form-input :type="type" :placeholder="placeholder" @change="changeValue($event)"></b-form-input>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  props : {
    name :  {type : String},
    title : {type : String},
    placeholder : {type : String},
    type : {type : String}
  },
  methods:{
    changeValue : function(event) {
      this.$parent.$parent[this.name] = event;
    }
  }
}
</script>

<style>
  label {
    font-weight: bold;
    text-align: left;
    margin-top: 20px;
  }
</style>