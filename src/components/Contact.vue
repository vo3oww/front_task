<template>
  <b-container fluid style="text-align: left">
    <b-row class="my-1">
      <b-col sm="3">
        <label>{{ title }}</label>
      </b-col>
    </b-row>
    <b-row class="my-1">
      <b-col sm="9">
        <b-form-input type="text" v-model="contact" :placeholder="placeholder" @change="changeValue($event)" @keyup="getPhoneMask(contact)" ></b-form-input>
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
  data: () => ({
    contact: null,
  }),
  methods:{
    changeValue : function(event) {
      const tel = event.replace(/[^0-9]/g, '')
      this.$parent.$parent[this.name] = tel;
    },
    getPhoneMask(val) {
      let res = this.getMask(val)
      this.contact = res
      //this.model.contact = this.contact.replace(/[^0-9]/g, '')
    },
    getMask( phoneNumber ) {
      if(!phoneNumber) return phoneNumber
      phoneNumber = phoneNumber.replace(/[^0-9]/g, '')

      let res = ''
      if(phoneNumber.length < 3) {
        res = phoneNumber
      } else {
        if(phoneNumber.substr(0, 2) == '02') {
          if(phoneNumber.length <= 5) { //02-123-5678
            res = phoneNumber.substr(0, 2) + '-' + phoneNumber.substr(2, 3)
          } else if(phoneNumber.length > 5 && phoneNumber.length <= 9) {//02-123-5678
            res = phoneNumber.substr(0, 2) + '-' + phoneNumber.substr(2, 3) + '-' + phoneNumber.substr(5)
          } else if(phoneNumber.length > 9) {//02-1234-5678
            res = phoneNumber.substr(0, 2) + '-' + phoneNumber.substr(2, 4) + '-' + phoneNumber.substr(6)
          }
        } else {
          if(phoneNumber.length < 8) {
            res = phoneNumber
          } else if(phoneNumber.length == 8) {
            res = phoneNumber.substr(0, 4) + '-' + phoneNumber.substr(4)
          } else if(phoneNumber.length == 9) {
            res = phoneNumber.substr(0, 3) + '-' + phoneNumber.substr(3, 3) + '-' + phoneNumber.substr(6)
          } else if(phoneNumber.length == 10) {
            res = phoneNumber.substr(0, 3) + '-' + phoneNumber.substr(3, 3) + '-' + phoneNumber.substr(6)
          } else if(phoneNumber.length > 10) { //010-1234-5678
            res = phoneNumber.substr(0, 3) + '-' + phoneNumber.substr(3, 4) + '-' + phoneNumber.substr(7)
          }
        }
      }
      return res
    }
  }
}
</script>