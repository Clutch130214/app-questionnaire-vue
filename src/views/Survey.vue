<template>
<!-- This snippet uses Font Awesome 5 Free as a dependency. You can download it at fontawesome.io! -->
<body>
  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h5 class="card-title text-center">Question : {{ numQuestion }}</h5>
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
export default {
  data () {
    return {
      numQuestion: 0,
      response: ''
    }
  }
}
// @ is an alias to /src
</script>
