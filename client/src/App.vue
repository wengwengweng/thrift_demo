<template>
  <div id="app">
    <h1>Thrift</h1>
    <div>
      <input type="text" placeholder="username" v-model="username" />
      <input type="text" placeholder="words" v-model="words" />
      <button v-on:click="submit">提交</button>
    </div>
    <div class="list" v-for="item in list">
      <div>
        <p>words: {{item.words}}</p>
        <p>name: {{item.name}}</p>
        <p>status: success</p>
        <p>date: {{String(new Date(parseInt(item.date)))}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      username: '',
      words: '',
      list: []
    }
  },
  methods: {
    submit: function(event) {
      fetch('http://localhost:3001/', {
          method: 'POST',
          mode: 'cors',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: this.username,
            words: this.words
          })
        })
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          this.list = data.content
        })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  font-size: 50px;
  color: #41B883;
  font-weight: bolder;
}
input,
button {
  padding: 0 10px;
  display: block;
  width: 200px;
  height: 22px;
  line-height: 20px;
  border-radius: 4px;
  border: 1px solid #E6E6E6;
  outline: none;
  margin: 20px auto;
}
button {
  background: #41B883;
  color: #fff;
  width: 220px;
  border: none;
  transition: all 0.5s;
}
button:hover {
  background: #35495E;
}

.list div{
  font-size: 10px;
  margin: 0 auto 20px auto;
  width: 200px;
  text-align: left;
  border-bottom: 1px solid #E6E6E6;
}
.list p{
  margin: 2px 0;
}
</style>
