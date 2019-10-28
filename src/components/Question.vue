<template>
  <div>
    <!-- Libellé de la question -->
    <h5 class="card-title text-center">Question : {{ question }}</h5>
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    question: String
  }
}
</script>
