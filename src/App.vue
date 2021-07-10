<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
<Form :model="d" :rules="rulesObj">
  <FormItem label="start" prop="d0">
    <Date-picker v-model="d.d0" clearable
                 @on-change="dtrChange" type="datetimerange" confirm placeholder="选择日期" style="width: 400px"></Date-picker>
  </FormItem>
  <Form-item label="end" prop="d1">
    <Date-picker v-model="d.d1" clearable
                 @on-change="dtrChange1" type="datetimerange" confirm placeholder="选择日期" style="width: 400px"></Date-picker>
  </Form-item>
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
              alert('d1 validating')
              if (v && v[0] === v[1]) {
                return cb()
              } else {
                return cb(new Error('YOU SHALL NOT PASS'))
              }
            },
            trigger: 'change'
          }
        ]
      },
      d: {d0: [], d1:[]}
    }
  },
  methods: {
    dtrChange(a){
      alert(JSON.stringify(a))
      this.d.d1=[new Date(new Date(a[0]).getTime() + 1000*60*60), new Date(new Date(a[0]).getTime() + 3000*60*60)]
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
