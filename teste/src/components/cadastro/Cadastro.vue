<template>
  <div>
    <h1 class="centralizado">Cadastro</h1>
    <br>
    <my-form class="testes"/>
    <br>
    <p>{{info_user}}<span></span></p>

  </div>
</template>

<script>
const coinbase = require('coinbase');

import Form from '../shared/loguin/Login.vue';

export default {
  components: {
    'my-form': Form
  },
  data () {
    return {
      info_user: [],
      key: '',
      secret: '',
    }
  },
  created() {

  },
  methods: {
    login: function() {
      const key = this.key
      const secret = this.secret

      if(key !== ''){
        var client   = new coinbase.Client({'apiKey': key, 'apiSecret': secret});

        client.getCurrentUser(function(err, data) {
          const info_user = data;
        });
      }else{
        console.log("Falha ao Conectar!")
      }
    }
  },
}

</script>
<style scoped>
    .centralizado {
        text-align: center;
    }
    *{
      font-family: "Roboto", sans-serif;
    }
</style>
