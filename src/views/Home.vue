<template>
<!-- This snippet uses Font Awesome 5 Free as a dependency. You can download it at fontawesome.io! -->
<body>
  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card card-signin my-5">
          <div class="card-body">
            <h5 class="card-title text-center">Rentrez vos informations</h5>
            <form class="form-signin">
              <div class="form-label-group">
                <input v-model="name" type="text" id="inputEmail" class="form-control" placeholder="Email address" required autofocus>
                <label for="inputEmail">Nom</label>
                <div class="mt-2">Value: {{ name }}</div>
              </div>
              <div class="form-label-group">
                <input v-model="firstName" type="text" id="inputPassword" class="form-control" placeholder="Password" required>
                <label for="inputPassword">Prénom</label>
                <div class="mt-2">Value: {{ firstName }}</div>
              </div>
              <div class="form-label-group">
                <input v-model="society" type="text" id="inputSociety" class="form-control" placeholder="Society" required>
                <label for="inputSociety">Entreprise</label>
                <div class="mt-2">Value: {{ society }}</div>
              </div>
              <router-link to="/survey">
                <button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Commencez le test</button>
              </router-link>
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
      name: '',
      firstName: '',
      society: ''
    }
  }
}
// @ is an alias to /src
</script>
