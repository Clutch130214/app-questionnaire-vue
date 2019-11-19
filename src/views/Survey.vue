
<template>
<body>
  <div class="container" v-cloak>
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <div v-if="this.questionnaire.questions && !this.surveyIsFinish">
              <!-- Composant Question -->
              <Question :question = this.questionnaire.questions[numQuestion].question ></Question>
                <b-form-group>
                  <b-form-radio-group
                    v-model="selected"
                    :options="getResponse()"
                    name="radios-stacked"
                    stacked
                  ></b-form-radio-group>
                </b-form-group>
                <div v-on:click="addResponse()">
                  <button class="btn btn-lg btn-primary btn-block text-uppercase">Validez</button>
                </div>
            </div>
            <div v-if="this.surveyIsFinish">
              <Result :result = this.getNbGoodResponse() :questionnaire = this.questionnaire.questions :summary = this.responseSelected ></Result>
              <div class="padding-left-1 align-left">
                  <router-link to="/home"><button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Retour à l'accueil</button></router-link>
              </div>
            </div>
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
import Result from '../components/Result.vue'
import Questionnaire from '../bddJson/Questionnaire.json'
import PouchDB from 'pouchdb'
var db = new PouchDB('questionnaire_db') // Création de la connection à la BDD : 28/10/2019
var url = 'http://localhost:5984/questionnaire_db' // Initialisation de l'url de ma base de données : 28/10/2019
db.replicate.from(url)

export default {
  components: {
    Question,
    Result
  },
  data () {
    return {
      numQuestion: 0,
      selected: '',
      questionnaire: Questionnaire,
      responseSelected: [],
      surveyIsFinish: false
    }
  },
  methods: {
    addResponse: function () {
      if (this.selected !== '') {
        if (this.numQuestion + 1 >= this.questionnaire.questions.length) {
          const objResponse = this.questionnaire.questions[this.numQuestion].responses.find(r => r.value === this.selected)
          this.responseSelected.push(objResponse)
          this.selected = ''
          this.surveyIsFinish = true
          var result = {
            _id: 'result_' + this.$route.query.user,
            idUser: this.$route.query.user,
            nbgoodResponses: this.getNbGoodResponse(),
            nbQuestions: this.questionnaire.questions.length
          }
          db.put(result).then(function (doc) {
            console.log(doc)
          })
        } else {
          const objResponse = this.questionnaire.questions[this.numQuestion].responses
          this.responseSelected.push(objResponse.find(r => r.value === this.selected))
          this.selected = ''
          this.numQuestion = this.numQuestion + 1
        }
      } else {
        this.$bvToast.toast(`Veuillez sélectionner une reponse`, {
          title: `Saisie impossible`,
          toaster: 'b-toaster-bottom-center',
          variant: 'primary',
          solid: true,
          appendToast: true
        })
      }
    },
    loadSurvey: function () {
      db.get('Questionnaire').then((doc, err) => {
        this.questionnaire = doc
      })
    },
    getResponse: function () {
      const values = []
      this.questionnaire.questions[this.numQuestion].responses.map(r => {
        values.push(r.value)
      })
      return values
    },
    getNbGoodResponse: function () {
      return this.responseSelected.filter(r => r.goodResponse === true).length
    }
  }
}
// @ is an alias to /src
</script>
