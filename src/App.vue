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
            <input type="radio" :id="university.Name" :value="university" v-model="newProfile.University">
            <label :for="university.Name">{{university.Name}}</label>
          </div>
        </div>
        <hr>
        <div class="form-group">
          <div v-for="hall in Halls" v-if="hall.University==newProfile.University.Name">
            <input type="radio" :id="hall.Name" :value="hall" v-model="newProfile.Hall">
            <label :for="hall.Name">{{hall.Name}}</label>
          </div>
        </div>
        <hr>
        <div class="form-group">
          <div v-for="food in Foods" v-if="food.University==newProfile.University.Name">
            <input type="radio" :id="food.Type" :value="food" v-model="newProfile.Food">
            <label :for="food.Type">{{food.Type}}</label>
          </div>
        </div>
        <hr>
        <input type="submit" class="btn btn-primary" v-on:click="createChart('day', computedValue[0]); createChart('week', computedValue[1]); createChart('month', computedValue[2]); createChart('year', computedValue[3])" value="Add Profile">
      </form>
    </div>
    <div class="col-md-12 text-center">
      <hr>
      {{computedValue}}
    </div>
    <div v-if="show==true" class="col-md-12 text-center" >
      <div id="day" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="week" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="month" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="year" style="height: 500px; width: 100%;"></div>
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

let ProfilesRef = db.ref('Profiles')
let UniversitiesRef = db.ref('Universities')
let HallsRef = db.ref('Halls')
let FoodsRef = db.ref('Foods')

export default {
  name: 'app',
  
  data () {
    return {
      newProfile: {
          University : null,
          Hall : null,
          Food : null
      },
      show: true
    }
  },

  methods: {
    addProfile: function () {
      //ProfilesRef.push(this.newProfile)
      this.newProfile.University = null;
      this.newProfile.Hall = null;
      this.newProfile.Food = null;
      console.log('New Entry added')
    },
    removeProfile: function (entry) {
      ProfilesRef.child(entry['.key']).remove()
    },
    createChart: function (id, plotData) {
      var chart = new CanvasJS.Chart(id, {
        animationEnabled: true,
        title:{
          text: "",
          horizontalAlign: "center"
        },
        data: [{
          type: "doughnut",
          startAngle: 60,
          //innerRadius: 60,
          indexLabelFontSize: 17,
          indexLabel: "{label} - {y}",
          toolTipContent: "<b>{label}:</b> {y} (#percent%)",
          dataPoints: plotData
        }]
      });
      console.log(plotData)
      this.show=true;
      chart.render();
    }
  },

  computed: {
    reversedHalls: function () {
      return this.Halls.reverse()
    },
    computedValue: function() {
      let u = (this.newProfile.University == null) ? 0 : this.newProfile.University.Fee;
      let h = (this.newProfile.Hall == null) ? 0 : this.newProfile.Hall.Rent;
      let f = (this.newProfile.Food == null) ? 0 : this.newProfile.Food.Price;
      
      let day = [{y: u/365, label: "Tuition"}, {y: h/30, label: "Hostel"}, {y: f, label: "Food"}];  
      let week = [{y: u/56, label: "Tuition"}, {y: h/4.5, label: "Hostel"}, {y: f*7, label: "Food"}];
      let month = [{y: u/12, label: "Tuition"}, {y: h, label: "Hostel"}, {y: f*30, label: "Food"}];
      let year = [{y: u, label: "Tuition"}, {y: h*12, label: "Hostel"}, {y: f*365, label: "Food"}];
      
      return [day, week, month, year];
    }
  },
  components: {

  },
  firebase: {
    Profiles: ProfilesRef,
    Universities: UniversitiesRef,
    Halls: HallsRef,
    Foods: FoodsRef
  },
}


</script>


<style>
</style>