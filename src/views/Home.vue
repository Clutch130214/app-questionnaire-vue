<template>
<body>
  <div class="container">
    <div class="padding-right-1 align-right">
        <router-link to="/login"><b-button variant="primary">Se connecter</b-button></router-link>
    </div>
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h5 class="card-title text-center">Rentrez vos informations</h5>
              <div class="form-label-group">
                <input v-model="name" type="text" id="inputEmail" class="form-control" placeholder="Email address" required autofocus>
                <label for="inputEmail">Nom</label>
              </div>
              <div class="form-label-group">
                <input v-model="firstName" type="text" id="inputPassword" class="form-control" placeholder="Password" required>
                <label for="inputPassword">Prénom</label>
              </div>
              <div class="form-label-group">
                <input v-model="society" type="text" id="inputSociety" class="form-control" placeholder="Society" required>
                <label for="inputSociety">Entreprise</label>
              </div>
              <button v-on:click="addCandidate()" class="btn btn-lg btn-primary btn-block text-uppercase">Commencez le test</button>
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

import PouchDB from 'pouchdb'
var db = new PouchDB('questionnaire_db') // Création de la connection à la BDD : 28/10/2019
var url = 'http://localhost:5984/questionnaire_db' // Initialisation de l'url de ma base de données : 28/10/2019
db.replicate.to(url)

export default {
  data () {
    return {
      name: '',
      firstName: '',
      society: ''
    }
  },
  methods: {
    addCandidate: function () {
      if (this.name !== '' || this.firstName !== '' || this.society !== '') {
        var candidate = {
          _id: 'user_' + this.name,
          name: this.name,
          firstName: this.firstName,
          society: this.society
        }
        var vm = this
        db.put(candidate).then(function (doc) {
          vm.$router.push({ path: '/survey', query: { user: doc.id } })
        })
      } else {
        this.$bvToast.toast(`Veuillez remplir tout les champs`, {
          title: `Saisie impossible`,
          toaster: 'b-toaster-bottom-center',
          variant: 'primary',
          solid: true,
          appendToast: true
        })
      }
    }
  }
}
// @ is an alias to /src
</script>
