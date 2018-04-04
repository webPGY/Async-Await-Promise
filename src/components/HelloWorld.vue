<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>打开控制台看打印效果</h2>
    <h3>代码详见HelloWorld.vue</h3>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Async&&Await'
    }
  },
  methods: {
    getTimeout (time) {
      return new Promise(resolve => {
        setTimeout(() => {
          resolve(time + 200)
        }, time)
      })
    },
    runstep1 (a) {
      console.log(`runstep1 with ${a}`)
      return this.getTimeout(a)
    },
    runstep2 (a, b) {
      console.log(`runstep2 with ${a} and ${b}`)
      return this.getTimeout(a + b)
    },
    runstep3 (a, b, c) {
      console.log(`runstep3 with ${a},${b} and ${c}`)
      return this.getTimeout(a + b + c)
    },
    result (val) {
      return new Promise((resolve, reject) => {
        val < 3000 ? resolve(`执行时间为:${val}`) : reject(new Error(`执行时间为:${val}`))
      })
    },
    async run () {
      console.time('run')
      const time1 = 300
      const time2 = await this.runstep1(time1)
      const time3 = await this.runstep2(time1, time2)
      const time4 = await this.runstep3(time1, time2, time3)
      this.result(time4).then(res => {
        console.log('Quickly', res)
      }).catch(err => {
        console.log('Timeout', err)
      })
      console.log(`the result is ${time4}`)
      console.timeEnd('run')
    }
  },
  mounted () {
    this.run()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
