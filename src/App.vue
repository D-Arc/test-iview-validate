<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
<Form :model="d" :rules="rulesObj">
  <FormItem label="start" prop="d0">
    <Date-picker v-model="d.d0" clearable :editable="false"
                 @on-change="dtrChange(true)" type="datetimerange" confirm placeholder="选择日期" style="width: 400px"></Date-picker>
  </FormItem>
  <FormItem label="end" prop="d1">
    <Date-picker v-model="d.d1" clearable :editable="false"
                 @on-change="dtrChange(false)" type="datetimerange" confirm placeholder="选择日期" style="width: 400px"></Date-picker>
  </FormItem>
</Form>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      rulesObj: {
        d0: [
          { required: true, message: '不能为空', trigger: 'change' }
        ],
        d1: [
          {
            validator: (r, v, cb) => {
              console.log(v)
              if (!v || !v[0] || !v[1]) {
                alert('d1 validating 不能为空')
                cb(new Error('不能为空'))
                // return
              }
              if (v[0].getFullYear() !== v[1].getFullYear() ||
                      v[0].getMonth() !== v[1].getMonth() ||
                      v[0].getDate() !== v[1].getDate()
              ) {
                alert('d1 validating Y S N P')
                cb(new Error('YOU SHALL NOT PASS'))
                // return
              }
              alert('VALID')
              cb()
            },
            trigger: 'change'
          }
        ]
      },
      d: {
        d0: [],
        d1: []
      }
    }
  },
  methods: {
    dtrChange(isStart){
      const a = isStart ? this.d.d0 : this.d.d1
      if (isStart) {
        this.d.d1=[
          new Date(new Date(a[0]).getTime() + 8000*60*60),
          new Date(new Date(a[1]).getTime() + 8000*60*60)
        ]
      } else {
        this.d.d0=[
          new Date(new Date(a[0]).getTime() - 8000*60*60),
          new Date(new Date(a[1]).getTime() - 8000*60*60)
        ]
      }
    },
    dtrChange1(a) {
      alert('second' + JSON.stringify(a))
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
