<template>
  <div class='cont-enter-number cont-terminal d-flex flex-column'>
    <div class='mt-auto mb-auto'>
    	<div class='title'>Пополнение счета на {{itemOper.title || $route.params.name}} </div>
      <div class='d-flex justify-content-center cont-tel'>
        <div class='num'>+7</div>
        <div v-for="(num, key, index) in lenNumber" :key="key" class='num'>
          {{ key == 0 ? '(' : ''}}
          {{arrNumber[num] ? arrNumber[num] : '_'}}
          {{ key == 2 ? ')' : ''}}
          {{ key == 5 || key == 7 ? ' - ' : ''}}
        </div>
      </div>
      <div class='cont-btn-num'>
        <button type='button' class='btn-num' value='1'  v-on:click='incAge'> 1 </button>
        <button type='button'  class='btn-num' value='2'  v-on:click='incAge'> 2 </button>
        <button type='button'  class='btn-num' value='3'  v-on:click='incAge'> 3 </button><br>
        <button type='button'  class='btn-num' value='4'  v-on:click='incAge'> 4 </button>
        <button type='button'  class='btn-num' value='5'  v-on:click='incAge'> 5 </button>
        <button type='button'  class='btn-num' value='6'  v-on:click='incAge'> 6 </button><br>
        <button type='button' class='btn-num'  value='7'  v-on:click='incAge'> 7 </button>
        <button type='button'  class='btn-num' value='8'  v-on:click='incAge'> 8 </button>
        <button type='button'  class='btn-num' value='9'  v-on:click='incAge'> 9 </button><br>
        <button type='button'  class='btn-num' v-on:click='clearNum'> C </button>
        <button type='button'  class='btn-num' value='0'  v-on:click='incAge'> 0 </button>
        <button type='button'  class='btn-num' v-on:click='delNum'> &lt; </button>
      </div>
    </div>
    <div class='footer '>
      <div class='cont-footer  w-100'>
        <router-link to="/" class='btn btn-back'> Назад </router-link>
        <router-link to="/" class='btn btn-menu ml-auto mr-auto'>Главная</router-link>
    	  <router-link :to="'/enterAmount/' + $route.params.name +'/'+arrNumber.join('')" operator='$route.params.name' class='btn btn-next-page' :class='{disabled: arrNumber.length <= lenNumber }'>Оплатить </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EnterNumber',

  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      itemOper: null,
      arrNumber: [],
      lenNumber: 10
    }
  },
  created: function () {
    this.$parent.setOperator(this.$route.params.name)
    this.itemOper = this.$parent.itemOper
  },
  methods: {
    incAge (event) {
      if (this.arrNumber.length > this.lenNumber) return
      var val = event.target.value
      this.arrNumber.push(val)
    },
    clearNum () {
      this.arrNumber = []
    },
    delNum () {
      this.arrNumber.pop()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang='scss'>
@import '../sass/default.scss';
@import '../sass/enterNumber.scss';
</style>
