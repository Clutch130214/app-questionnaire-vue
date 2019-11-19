<template>
<body>
  <div class="padding-left-1 align-left">
      <router-link to="/home"><b-button variant="primary">Revenir à l'accueil</b-button></router-link>
  </div>
  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h5 class="card-title text-center">Bienvenu sur votre espace d'administration</h5>
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
var db = new PouchDB('questionnaire_db') // Création de la connection à la BDD
var url = 'http://localhost:5984/questionnaire_db' // Initialisation de l'url de ma base de données
db.replicate.from(url)

export default {
  data () {
    return {
      users: []
    }
  }
}
// @ is an alias to /src
</script>
