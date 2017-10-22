<template>
  <div id="app">
    <div class="jumbotron">
      <h1>PreparedForU</h1>
    </div>

<!--     <div class="container">
      <div v-for="entry in entries" class="card text-center" style="margin:30px;">
          <div class="card-header">
            Journal Entry
          </div>
          <div class="card-body">
            <h4 class="card-title">{{entry.title}}</h4>
            <p class="card-text">{{entry.content}}</p>
          </div>
          <div class="card-footer text-muted">
            {{entry.date}}
          </div>
      </div>
    </div> -->

    <div class="container">
      <div v-for="entry in reversedHalls" class="card text-center" style="margin:30px;">
          <div class="card-header">
            Hall of Residence
          </div>
          <div class="card-body">
            <h4 class="card-title">{{entry.HallName}}</h4>
            <p class="card-text">{{entry.SingleRoomRent}}</p>
            <p class="card-text">{{entry.DoubleRoomRent}}</p>
          </div>
          <div class="card-footer text-muted">
            {{entry.University}}
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

let entryRef = db.ref('Halls')

export default {
  name: 'app',
  firebase: {
    Halls: entryRef
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