<template>
  <div id="app">
    <div class="jumbotron">
      <h1>PreparedForU</h1>
    </div>

    <div class="container">
      <div v-for="entry in Halls" v-if="entry.University=='Nanyang Technological University'">
          <div class="col-md-4 col-md-offset-4">
            <a href="" class="btn btn-block btn-default">{{entry.HallName}}</a>
          </div>
      </div>
    </div>

  </div>
</template>


<script>

import Firebase from 'firebase'

let config = {
  apiKey: "AIzaSyCzrPQzAKBOX_Q61ymwfp0K4CgcLp3mUFA",
  authDomain: "cz2006-e021a.firebaseapp.com",
  databaseURL: "https://cz2006-e021a.firebaseio.com",
  projectId: "cz2006-e021a",
  storageBucket: "cz2006-e021a.appspot.com",
  messagingSenderId: "674471346840"
}

let app = Firebase.initializeApp(config)
let db = app.database()

let UniversitiesRef = db.ref('1/Universities')
let HallsRef = db.ref('2/Halls')

export default {
  name: 'app',
  firebase: {
    Universities: UniversitiesRef,
    Halls: HallsRef
  },
  computed: {
    reversedHalls: function () {
      return this.Halls.reverse()
    }
  },
  components: {

  }
}


</script>


<style>

.jumbotron{
  text-align: center;
  background-color: white;

}
.jumbotron h1{
  font-family: 'Lato';
  font-weight: 300;
}


</style>