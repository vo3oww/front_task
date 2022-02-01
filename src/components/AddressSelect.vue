<template>
  <div class="m-4">
    <div class="m-4">
      <b-form-select ref="addr1" @change="changeAddr1($event)" v-bind:options="addr1List" required="required"></b-form-select>
    </div>
    <div class="m-4">
      <b-form-select ref="addr2" @change="changeAddr2($event)" v-bind:options="addr2List"></b-form-select>
    </div>
    <div class="m-4">
      <b-form-select ref="addr3" @change="changeAddr3($event)" v-bind:options="addr3List"></b-form-select>
    </div>
  </div>
</template>

<script>

import axios from "axios";

const requestGetAddr = function(param, target){
  axios.get("https://grpc-proxy-server-mkvo6j4wsq-du.a.run.app/v1/regcodes?is_ignore_zero=true&regcode_pattern="+param).then((res)=>{
    let data = undefined;
    let list = res.data.regcodes;
    
    target.splice(0,target.length);
    for(let i = 0; i < list.length; i++) {
      data = list[i];
      target.push({
        text : data["name"]
        ,value : data["code"]
      })
    }
  });
}
export default {
  mounted() {
    this.initAddr1();
  },
  methods:{
    initAddr1 : function () {
      this.addr2List.splice(0,this.addr2List.length);
      this.addr3List.splice(0,this.addr3List.length);
      requestGetAddr("*00000000",this.addr1List)
    },
    changeAddr1 : function(event,obj) {
      const text = obj;
      console.log(text);
      let searchParam = event;
      searchParam = searchParam.replace(/(\d{2})(\d{2})(\d{6})/,"$1*$3")
      this.addr3List.splice(0,this.addr3List.length);
      requestGetAddr(searchParam,this.addr2List)
      this.$parent.addr1 = event;
    },
    changeAddr2 : function(event) {
      let searchParam = event;
      searchParam = searchParam.replace(/(\d{2})(\d{2})(\d{6})/,"$1$2*")
      requestGetAddr(searchParam,this.addr3List)
      this.$parent.addr2 = event;
    },
    changeAddr3 : function(event) {
      this.$parent.addr3 = event;
    }
  },
  data() {
    return {
      selected: null,
      addr1List : [],
      addr2List : [],
      addr3List : [],
      addr1 : "",
      addr2 : "",
      addr3 : ""
    }
  }
}
</script>