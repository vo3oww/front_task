<template>
  <div style="text-align: left">
    <b-form-checkbox
        id="checkbox-1"
        v-model="status"
        name="checkbox-1"
        value="accepted"
        @change="change($event)"
        unchecked-value="not_accepted"
    >
      {{text}}
    </b-form-checkbox>
  </div>
</template>

<script>
export default {
  props : {
    text : {type : String},
    name : {type : String}
  },
  methods:{
    change : function(event){
      this.$parent.$parent[this.name] = event;
    }
  },
  data() {
    return {
      status: 'not_accepted'
    }
  }
}
</script>