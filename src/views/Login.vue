<template>
<body>
  <div class="padding-left-1 align-left">
      <router-link to="/home"><b-button variant="primary">Retour</b-button></router-link>
  </div>
  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h5 class="card-title text-center">Rentrez vos Identifiant</h5>
            <form class="form-signin">
              <div class="form-label-group">
                <input v-model="login" type="text" id="inputEmail" class="form-control" placeholder="Email address" required autofocus>
                <label for="inputEmail">Identifiant</label>
              </div>
              <div class="form-label-group">
                <input v-model="mdp" type="password" id="inputPassword" class="form-control" placeholder="Password" required>
                <label for="inputPassword">Mot de passe</label>
              </div>
              <button v-on:click="connect()" class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Se connecter</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</body>
</template>

<style lang="scss">
@import '../css/style.css';
</style>

<script>

export default {
  data () {
    return {
      login: '',
      mdp: ''
    }
  },
  methods: {
    connect: function () {
      var vm = this
      vm.$router.push('/admin')
    }
  }
}
// @ is an alias to /src
</script>
