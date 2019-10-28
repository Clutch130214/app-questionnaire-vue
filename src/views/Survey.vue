
<template>
<body>
  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <!-- Composant Question -->
            <Question :question = question[numQuestion] ></Question>
            <form class="form-signin">
              <div class="form-label-group">
                <input v-model="response" type="text" id="inputEmail" class="form-control" placeholder="Response" required autofocus>
                <label for="inputEmail">Reponse</label>
                <div class="mt-2">Value: {{ response }}</div>
              </div>
              <div v-on:click="numQuestion = numQuestion+1">
                <button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Validez</button>
              </div>
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
import Question from '../components/Question.vue'
import PouchDB from 'pouchdb'
var db = new PouchDB('questionnaire_db') // Création de la connection à la BDD : 28/10/2019
var url = 'http://localhost:5984/questionnaire_db' // Initialisation de l'url de ma base de données : 28/10/2019

export default {
  components: {
    Question
  },
  data () {
    return {
      numQuestion: 0,
      response: '',
      question: [
        'Le fromage',
        'Oui',
        'Obiwan Kenobi'
      ]
    }
  },
  methods: {
    addDB: function () {
      var todo = {
        _id: 'test'
      }
      db.put(todo).then(function (doc) {
        console.log(doc)
      })
      db.replicate.to(url)
    }
  }
}
// @ is an alias to /src
</script>
