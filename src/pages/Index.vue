<template>
  <q-page class="flex flex-center">
    <div v-if ="!win">
      <div class="box" v-for="(i,idx) in items" :key="idx">
        {{ i }}
      </div>
      <q-input v-model="ans" placeholder="共有多少?" @keyup.enter ="check()"/>
      <q-btn @click="check()">送出!</q-btn>
    </div>
    <div v-else>
      <div class="score">答對率{{Math.round(right / (right + wrong) * 100)}}%</div>
      <q-btn @click="resetAll()">重來!</q-btn>
    </div>
    <q-circular-progress
      :value="value"
      size="50px"
      :thickness="1"
      color="orange"
      track-color="grey-8"
      class="q-ma-md"
    /><q-circular-progress
      :value="right / (right + wrong) * 100"
      size="50px"
      :thickness="1"
      color="green"
      track-color="grey-8"
      class="q-ma-md"
    /><q-circular-progress
      :value="timer"
      size="50px"
      :thickness="1"
      color="red"
      track-color="grey-8"
      class="q-ma-md"
    />
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  props: ['l', 'n'],
  data () {
    return {
      items: [3,3,3,3],
      ans: null,
      value: 0,
      timer: 0,
      win: false,
      right: 0,
      wrong: 0
    }
  },
  methods: {
    go () {
      if (!this.win) {
        this.timer++
      }
      if (this.timer >= 100) {
        this.check()
        this.timer = 0
      }
    },
    check () {
      if (this.win) { return }
      if (this.ans == this.items[0] * this.items.length) {
        // alert('對了!')
        this.value += 10
        this.right++
        this.reset()
      } else {
        this.value += 10
        this.wrong++
      }
      if (this.value == 100) {
        this.win = true
        this.value = 0
      }
      this.timer = 0
    },
    reset() {
      this.win = false;
      this.ans = null;
      let l = Math.floor(Math.random()*this.l)+1
      let n = Math.floor(Math.random()*this.n)+1
      this.items = []
      for (var i = 0; i < l; i++) {
        this.items.push(n)
      }
    },
    resetAll() {
      this.right = 0;
      this.wrong = 0;
      this.reset()
    }
  },
  mounted () {
    this.reset()
    setInterval(this.go, 500)
  },
  watch: {
    l (val) {
      this.reset()
    },
    n (val) {
      this.reset()
    }
  }
}
</script>

<style type="text/css" scoped="">
  
  .box {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    height: 100px;
    font-size: 26px;
    border: 1px solid black;
  }

</style>
