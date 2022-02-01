<template>
  <div id="app">
    <b-form @submit="onSubmit" @reset="onReset">
      <div>
        <img src="./assets/logoImg.png">
        <p class="textCenter textBold textPurple"> 
          강남을 중심으로 열심히 운영하고 있어요.<br>소중한 의견 받아서 열심히 늘려 나갈게요! 
        </p>
      </div>

      <div class="m-4 textCenter">
        <AddressSelect id="address" ref="addr1"></AddressSelect>
      </div>

      <div class="m-4">
        <div class="mb-3">
          <a class="textLeft textBlack divMargin" v-b-toggle href="#infomationCollapse" @click.prevent>
            <hr>
            <p class="textBold">추가 정보 선택</p>
            <p class="">추가 정보를 등록해 주시면<br>최적의 공간을 찾아서 연락 드릴게요!</p>
            <hr>
          </a>
        </div>

        <b-collapse unvisible id="infomationCollapse">
          <div class="m-4">
            <DVSlider name="acreage" title="평수 (선택)" min=1 max=40 step=1 suffix="평" values="[1,10,20,30,40]"></DVSlider>
            <DVSlider name="amount" title="월세(29박 기준) (선택)" min=1 max=250 step=1 suffix="만원" postfix="만원~" values="[1,50,100,150,200,250]"></DVSlider>
          </div>

          <div class="m-4">
            <Input ref="name" name="name" title="이름 (선택)" type="text" placeholder="정규직"></Input>
            <Contact ref="tel" name="tel" title="휴대폰번호 (선택)" type="text" placeholder="010-1234-5678"></Contact>
            <Input ref="email" name="email" title="이메일 (선택)" type="text" placeholder="sarava@gmail.com"></Input>
          </div>

          <div class="my-1 m-4">
            <label>개인 정보 수집 및 이용 동의 (선택)</label>
            <div class="divBorder">
              <div class="m-3">
                <p>① 수집 및 이용목적 : 지역 수요 분석, 추가 설문</p>
                <p>② 수집정보 : 이름(성함), 휴대폰번호, 이메일</p>
                <p>③ 보유기간 : 제공동의일로부터 1년</p>
                <p>귀하께서는 개인정보 수집 및 이용에 대해 거부할 권리가 있습니다.</p>
              </div>
            </div>

            <CheckBox name="aggreement" text="개인정보 수집 및 이용에 동의합니다. (동의한 경우에만 개인 정보가 수집됩니다.)"></CheckBox>
          </div>
        </b-collapse>
      </div>

      <Button variant="primary" text="완료" type="submit"></Button>
    </b-form>
  </div>
</template>

<script>
  import AddressSelect from './components/AddressSelect.vue'
  import Input from './components/Input.vue'
  import CheckBox from './components/CheckBox.vue'
  import DVSlider from './components/DVSlider.vue'
  import Button from './components/Button.vue'
  import Contact from './components/Contact.vue'

  export default {
    name: 'App',
    props : [
      "name",
      "tel",
      "email",
      "addr1",
      "addr2",
      "addr3",
      "aggreement",
      "acreage",
      "amount"
    ],
    components: {
      AddressSelect,
      Input,
      CheckBox,
      DVSlider,
      Button,
      Contact
    },
    methods : {
      onReset : function(){

      },
      onSubmit : function(event){
        event.preventDefault();
        console.log(this.acreage)
        // TODO: validate
        const data = {
          addr1 : this.addr1,
          addr2 : this.addr2,
          addr3 : this.addr3,
          name : this.name,
          tel : this.tel,
          email : this.email,
          aggreement : this.aggreement,
          acreage : this.acreage,
          amount : this.amount
        }

        if(this.isCollopse 
            && ( (!data.name || !data.email || !data.tel || (!data.aggreement && data.aggreement == "not_accepted"))
            || ("" == data.name.trim() || "" == data.email.trim() || "" == data.tel.trim() || (!data.aggreement && data.aggreement == "not_accepted")))) {
          alert("추가 정보를 입력해주세요");
          return;
        }
        console.log(JSON.stringify(data))
      }
    }
  }
</script>

<style>
  .textBold {
    font-weight: bold
  }
  .textBlack {
    color:black;
  }
  .textPurple {
    color:mediumpurple;
  }
  .textCenter { 
    text-align: center
  }
  .textLeft { 
    text-align: left;
  }
  .divMargin {
    margin-left: 20px;
  }
  .divBorder {
    border: #2c3e50 solid 1px; 
    text-align: left;
  }

  a {
    text-decoration-line: none;
  }
  a:hover {
    text-decoration-line: none;
  }

  label {
    font-weight: bold;
    text-align: left;
    margin-top: 20px;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /* text-align: center; */
    color: #2c3e50;
    margin-top: 60px;
  }
</style>