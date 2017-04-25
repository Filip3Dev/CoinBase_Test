<template>
<div class="">

  <form @submit.prevent="login()">
    <div class="controle">
      <label for="key">Chave Primaria</label>
      <input id="key" v-model.lazy="key" autocomplete="off">
    </div>

    <div class="controle">
      <label for="secret">Chave Secreta</label>
      <input id="secret" autocomplete="off" v-model.lazy="secret">
    </div>

    <div class="controle">
      <button type="submit" name="button">Entrar</button>
    </div>

    <p>{{info_user}}</p>
    <p>{{teste}}</p>
  </form>

</div>
</template>

<script>
const coinbase = require('coinbase');
export default {

    data () {
      return {
        key: '',
        secret: '',
        info_user: {},
        teste: [],
      }
    },
    methods: {
      login() {
        const key = this.key
        const secret = this.secret
        if(key !== ''){
          var client   = new coinbase.Client({'apiKey': key, 'apiSecret': secret});
          client.getCurrentUser(function(err, data) {
           console.log("Result" + data);
          //  data => this.teste = Object.keys(data).map(key => data[key])
           (data => this.teste = data)
          //  (data => this.info_user.update(data))

          });
        }else{
          console.log("Falha ao Conectar!")
        }
      },
    },
}
</script>

<style scoped>

  .imagem-responsiva {

    width: 100%;
  }

</style>
