<template>
  <div id="app">
    <div class="jumbotron">
      <h1>PreparedForU</h1>
    </div>

    <div class="col-md-8 col-md-offset-2">
      <h3 class="card-title" style="text-align:center; font-family:'Lato';">New Entry</h3>
      <form id="form" v-on:submit.prevent="addEntry">
        <div class="form-group" style="margin-top:20px;">
          <label for="entryName">Name:</label>
          <textarea type="text" id="entryName" class="form-control" v-model="newEntry.Name" ></textarea>
        </div>
        <input type="submit" class="btn btn-primary" value="Add Entry">
      </form>
    </div>

    <div class="container">
      <div v-for="entry in Universities">
          <div class="col-md-4 col-md-offset-4">
            <a href="" class="btn btn-block btn-default"> <button v-on:click="removeEntry(entry)" >{{entry.Name}}</button></a>
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

  data () {
    return {
      newEntry: {
          Name : ''
      }
    }
  },

  methods: {
    addEntry: function () {
      UniversitiesRef.push(this.newEntry)
      this.newEntry.Name = ''
      location.reload()
    },
    removeEntry: function (entry) {
      UniversitiesRef.child(entry['.key']).remove()
    }
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