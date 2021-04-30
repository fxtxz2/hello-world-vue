<template>
  <div class="home">
    <div class="display-flex control-container">
      <div>
        <button v-on:click="login">Login</button>
        <button v-on:click="getFile">Get File</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
const axios = require('axios').default;

export default {
  name: 'Download',
  data() {
    return {
      name: 'Vue.js',
      url: 'hello'
    }
  },
  methods: {
    login: function () {
      const data = JSON.stringify({
        "account": "xxx",
        "password": "xxxx"
      });

      const config = {
        method: 'post',
        url: '/api/login',
        headers: {
          'Content-Type': 'application/json'
        },
        data: data
      };

      axios(config)
          .then(function (response) {
            console.log(JSON.stringify(response.data));
          })
          .catch(function (error) {
            console.log(error);
          });
    },
    getFile: function () {
      const config = {
        method: 'get',
        url: '/api/common/downloadFile?xxxx.srt',
        headers: {
          'xxxx': 'xxxx'
        },
        responseType: 'blob'
      };
      axios(config).then(response => {
        const url = window.URL.createObjectURL(new Blob([response.data]));
        const link = document.createElement('a');
        link.href = url;
        link.setAttribute('download', 'xxxx.srt');
        document.body.appendChild(link);
        link.click();

      })
    }
  }
}
</script>
<style scoped>
.control-container {
  position: fixed;
  z-index: 999999;
}
.display-flex {
  display: flex;
}
</style>


