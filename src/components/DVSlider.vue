<template>
  <div>
    <div class="my-1 m-4">
      <label>{{title}}</label>
      <veeno
          v-on:change="change($event)"
          tooltips
          connect
          :options = "{start : [1,10]}"
          :pipsy = "{
            mode: 'values',
            density: 10,
            values: pipValue,
            format: {
                // 'to' Format the value to currency.
                to: function (value) {
                  if(postfix && value == range.max)
                    return value.toFixed(0) + ' ' + postfix;
                  else
                    return value.toFixed(0) + ' ' + suffix;
                },
                // 'from' Convert currency value to number.
                // Receives a string, should return a number.
                from: function (value) {
                    return Number(value.replace(' ' + suffix));
                }
            }
          }"
          :step = stepValue
          :range = range
      />
    </div>
  </div>
</template>

<script>
import veeno from 'veeno';

export default {
  props :{
    name : {type : String},
    title : {type : String},
    min: {type : String},
    max: {type : String},
    step: {type : String},
    suffix: {type : String},
    postfix: {type : String},
    values : {type : String}
  },
  data() {
    return {
      range : {
        min : parseInt(this.min,10),
        max : parseInt(this.max,10)
      },
      stepValue : parseInt(this.step,10),
      pipValue : eval(this.values)
    };
  },
  methods:{
    change : function (event) {
      const _this = this;
      this.$parent.$parent[this.name] = event.values.map(function(data){
        return data.replace(_this.suffix,"").replace(_this.postfix, "");
      });
    }
  },
  components: {
    veeno
  }
};
</script>

<style scoped>
  label {
    font-weight: bold;
    text-align: left;
    margin-top: 20px;
  }
</style>
