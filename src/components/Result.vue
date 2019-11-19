<template>
  <div>
    <h5 class="card-title text-center">Resultat : {{ result }} / {{ questionnaire.length }}</h5>
      <b-list-group>
        <!-- Liste des questions -->
        <div v-for="question in questionnaire" :key="question.id">
          <b-list-group-item>
            <div>
              <!-- Libellé de la question -->
              <h5>{{ question.question }}</h5>
            </div>
            <!-- Liste des reponses de la question -->
            <div v-for="response in question.responses" :key="response.id">
              <b-list-group>
                <b-list-group-item v-bind:variant="[getResponseColor(response, question, summary)]">
                  <!-- Libellé de la reponse -->
                  {{ response.value }}
                  <b-badge v-bind:variant="[getResponseColor(response, question, summary)]" pill>{{getIndicator(response, question, summary)}}</b-badge>
                </b-list-group-item>
              </b-list-group>
            </div>
          </b-list-group-item>
        </div>
      </b-list-group>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    result: Number,
    questionnaire: Number,
    summary: Array
  },
  methods: {
    // Fonction qui renvoie une couleur differente en fonction du type de la question (bonne, mauvaise ou non sélectionner)
    getResponseColor: function (response, question, summary) {
      const responseInSummary = summary.find(s => s.id === response.id && s.idQuestion === question.id)
      if (response.goodResponse) {
        return 'success'
      }
      if (responseInSummary) {
        if (responseInSummary.goodResponse) {
          return 'success'
        } else {
          return 'danger'
        }
      } else {
        return 'dark'
      }
    },
    // Fonction qui renvoie un indicateur ✓ si la reponse est bonne, ✗ si la reponse est mauvaise
    getIndicator: function (response, question, summary) {
      const responseInSummary = summary.find(s => s.id === response.id && s.idQuestion === question.id)
      if (responseInSummary) {
        if (responseInSummary.goodResponse) {
          return '✓'
        } else {
          return '✗'
        }
      } else {
        return ''
      }
    }
  }
}
</script>
