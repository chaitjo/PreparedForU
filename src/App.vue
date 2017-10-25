<template>
  <div id="app">
    <div style="text-align:center; font-family:'Lato';">
      <h1>PreparedForU</h1>
    </div>

    <div class="col-md-8 col-md-offset-2">
      <h3 class="card-title" style="text-align:center; font-family:'Lato';">New Profile</h3>
      <form id="form" v-on:submit.prevent="addProfile">
        <div class="form-group">
          <div v-for="university in Universities">
            <input type="radio" :id="university.Name" :value="university.Name" v-model="newProfile.University">
            <label :for="university.Name">{{university.Name}}</label>
          </div>
        </div>
        <hr>
        <div class="form-group">
          <div v-for="hall in Halls" v-if="hall.University==newProfile.University">
            <input type="radio" :id="hall.HallName" :value="hall.HallName" v-model="newProfile.Hall">
            <label :for="hall.HallName">{{hall.HallName}}</label>
          </div>
        </div>
        <hr>
        <input type="submit" class="btn btn-primary" v-on:click="addProfile" value="Add Profile">
      </form>
    </div>

    <div class="container">
      <div v-for="entry in Profiles">
          <div class="col-md-4 col-md-offset-4">
            <button class="btn btn-default" v-on:click="removeProfile(entry)" >{{entry.University}},{{entry.Hall}}</button>
          </div>
      </div>
    </div>

    <div>
      {{newProfile.University}}
      {{newProfile.Hall}}
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

let ProfilesRef = db.ref('1/Profiles')
let UniversitiesRef = db.ref('2/Universities')
let HallsRef = db.ref('3/Halls')

export default {
  name: 'app',
  

  data () {
    return {
      u: '',
      h: '',
      newProfile: {
          University : '',
          Hall : ''
      }
    }
  },

  methods: {
    addProfile: function () {
      ProfilesRef.push(this.newProfile)
      this.newProfile.University = '';
      this.newProfile.Hall = '';
      console.log('New Entry added')
      location.reload()
    },
    removeProfile: function (entry) {
      ProfilesRef.child(entry['.key']).remove()
    }
  },

  computed: {
    reversedHalls: function () {
      return this.Halls.reverse()
    }
  },
  components: {

  },
  firebase: {
    Universities: UniversitiesRef,
    Halls: HallsRef,
    Profiles: ProfilesRef
  },
}


</script>


<style>
</style>