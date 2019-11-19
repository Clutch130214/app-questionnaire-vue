<template>
  <div>
    <h5 class="card-title text-center">Resultat : {{ result }} / {{ questionnaire.length }}</h5>
      <b-list-group>
        <div v-for="question in questionnaire" :key="question.id">
          <b-list-group-item>
            <div>
              <h5>{{ question.question }}</h5>
            </div>
            <div v-for="response in question.responses" :key="response.id">
              <b-list-group>
                <b-list-group-item v-bind:variant="[getResponseColor(response, question, summary)]">{{ response.value }}</b-list-group-item>
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
    }
  }
}
</script>
