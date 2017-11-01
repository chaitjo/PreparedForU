<template>
  <div id="app">
    <div style="text-align:center;">
      <h1>PreparedForU</h1>
    </div>

    <div class="col-md-8 col-md-offset-2">
      <h3 style="text-align:center;">New Profile</h3>
      <form id="form" v-on:submit.prevent="addProfile">
        
        <div class="form-group">
          <div>
            <h4>Select your university</h4>
          </div>
          <div v-for="university in universities">
            <input type="radio" :id="university.fullName" :value="university.value" v-model="newProfile.university">
            <label :for="university.fullName">{{university.fullName}}</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.university">
          <div>
            <h4>What is your citizenship status?</h4>
          </div>
          <div v-for="citizenship in citizenships">
            <input type="radio" :id="citizenship.citizenship" :value="citizenship.value" v-model="newProfile.citizenship">
            <label :for="citizenship.citizenship">{{citizenship.citizenship}}</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.citizenship">
          <div>
            <h4>Select your course</h4>
          </div>
          <div v-for="course in courses" v-if="course.university==newProfile.university && course.citizenship==newProfile.citizenship">
            <input type="radio" :id="course.course" :value="course" v-model="newProfile.course">
            <label :for="course.course">{{course.course}}</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.university">
          <div>
            <h4>Will you be staying in on-campus housing?</h4>
          </div>
          <div>
            <input type="radio" id="Yes" value="true" v-model="newProfile.stayingOnCampus">
            <label for="Yes">Yes</label>
            <input type="radio" id="No" value="false" v-model="newProfile.stayingOnCampus">
            <label for="No">No</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.stayingOnCampus=='true'">
          <div>
            <h4>Will you usually be living on-campus during weekends as well?</h4>
          </div>
          <div>
            <input type="radio" id="Yes" value="true" v-model="newProfile.stayingOnCampusWeekends">
            <label for="Yes">Yes</label>
            <input type="radio" id="No" value="false" v-model="newProfile.stayingOnCampusWeekends">
            <label for="No">No</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.stayingOnCampus=='true'">
          <div>
            <h4>Select your room type</h4>
          </div>
          <div>
            <input type="radio" id="Single" value="Single" v-model="newProfile.roomOccupancy">
            <label for="Single">Single Occupancy</label>
            <input type="radio" id="Double" value="Double" v-model="newProfile.roomOccupancy">
            <label for="Double">Double Occupancy</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.roomOccupancy">
          <div>
            <h4>Will your room be equiped with an air conditioner</h4>
          </div>
          <div>
            <input type="radio" id="Yes" value="Yes" v-model="newProfile.roomAirCon">
            <label for="Yes">Yes</label>
            <input type="radio" id="No" value="No" v-model="newProfile.roomAirCon">
            <label for="No">No</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.roomOccupancy">
          <div>
            <h4>Select your hall</h4>
          </div>
          <div v-for="hall in halls" v-if="hall.university==newProfile.university && newProfile.roomOccupancy==hall.occupancy && newProfile.roomAirCon==hall.airCon">
            <input type="radio" :id="hall.hall" :value="hall" v-model="newProfile.hall">
            <label :for="hall.hall">{{hall.hall}}</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.stayingOnCampus=='false' || newProfile.stayingOnCampusWeekends=='false'">
          <div>
            <h4>Set your home location</h4>
          </div>
          <div>
            <input type="text" id="home" placeholder="Enter Postal Code" v-model="newProfile.home">
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.home">
          <div>
            <h4>What will be your usual mode of transport from home?</h4>
          </div>
          <div>
            <input type="radio" id="public" value="public" v-model="newProfile.transport">
            <label for="public">Public Transport</label>
            <input type="radio" id="taxi" value="taxi" v-model="newProfile.transport">
            <label for="taxi">Taxi</label>
            <input type="radio" id="personal" value="personal" v-model="newProfile.transport">
            <label for="personal">Personal Vehicle</label>
          </div>
          <hr>
        </div>
        
        <div class="form-group" v-if="newProfile.university">
          <div>
            <h4>Select your dietary preference</h4>
          </div>
          <div v-for="meal in meals" v-if="meal.university==newProfile.university">
            <input type="radio" :id="meal.diet" :value="meal" v-model="newProfile.meal">
            <label :for="meal.diet">{{meal.diet}}</label>
          </div>
          <hr>
        </div>

        <div class="form-group" v-if="newProfile.home">
          <div>
            <h4>Will you usually be having breakfast/dinner on campus or at home?</h4>
          </div>
          <div>
            <input type="radio" id="campus" value="false" v-model="newProfile.foodAtHome">
            <label for="campus">On campus</label>
            <input type="radio" id="home" value="true" v-model="newProfile.foodAtHome">
            <label for="nonveg">At home</label>
          </div>
          <hr>
        </div>
        
        <input type="submit" class="btn btn-primary" v-on:click="govDataAPI('e1c20915-ab7c-4bf9-bbbd-0197bbc7b98c'); createChart('daily', financialBreakdown[0]); createChart('weekly', financialBreakdown[1]); createChart('monthly', financialBreakdown[2]); createChart('semesterly', financialBreakdown[3])" value="Add Profile">
      
      </form>
    </div>

    <div class="col-md-12 text-center" style="margin-top: 50px;">
      {{newProfile}}
      <hr>
      {{financialBreakdown}}
      <hr>
      {{temp_data}}
    </div>
    
    <div class="col-md-12 text-center">
      <div id="daily" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="weekly" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="monthly" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="semesterly" style="height: 500px; width: 100%;"></div>
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

let profilesRef = db.ref('profiles')
let universitiesRef = db.ref('universities')
let citizenshipsRef = db.ref('citizenships')
let coursesRef = db.ref('courses')
let hallsRef = db.ref('halls')
let mealsRef = db.ref('meals')

export default {
  name: 'app',
  
  data () {
    return {
      newProfile: {
          university : null,
          citizenship : null,
          course : null,
          stayingOnCampus : null,
          stayingOnCampusWeekends : null,
          roomOccupancy : null,
          roomAirCon : null,
          hall : null,
          home : null,
          meal : null,
          foodAtHome : null,
      },
      temp_data : null
    }
  },

  methods: {
    addProfile: function () {
      //profilesRef.push(this.newProfile)
      this.newProfile.university = null;
      this.newProfile.hall = null;
      this.newProfile.meal = null;
      console.log('New Entry created')
      //location.reload()
    },
    removeProfile: function (entry) {
      profilesRef.child(entry['.key']).remove()
    },
    myGovDataAPI: function (resource_id) {
      let url = "https://data.gov.sg/api/action/datastore_search?resource_id=" + resource_id;
      axios.get(url).then((response) => {
        this.temp_data = response.data.result.records;
      }).catch( error => { console.log(error); });
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
      chart.render();
    }
  },

  computed: {
    financialBreakdown: function() {
      let tuitionFee = 0;
      if (this.newProfile.course!=null) {
        tuitionFee = this.newProfile.course.fee;
      }

      let hallRent = 0;
      if (this.newProfile.hall!=null) {
        hallRent = this.newProfile.hall.rent;
      }

      let breakfastCost = 0;
      if (this.newProfile.meal!=null && !(this.newProfile.home=='true' && this.newProfile.foodAtHome=='true')) {
        breakfastCost = this.newProfile.meal.breakfast;
      }
      
      let lunchCost = 0;
      if (this.newProfile.meal!=null) {
        lunchCost = this.newProfile.meal.lunch;
      }

      let dinnerCost = 0;
      if (this.newProfile.meal!=null && !(this.newProfile.home=='true' && this.newProfile.foodAtHome=='true')) {
        dinnerCost = this.newProfile.meal.dinner;
      }

      let transportCost = 0;
      
      let daily = [
        {y: tuitionFee/(30.5*5), label: "Tuition Fee"},
        {y: hallRent/30.5, label: "Hall Rent"},
        {y: breakfastCost, label: "Breakfast"},
        {y: lunchCost, label: "Lunch"},
        {y: dinnerCost, label: "Dinner"},
        {y: transportCost, label: "Transport Cost"}
      ]

      let weekly = [
        {y: tuitionFee/(30.5*5/7), label: "Tuition Fee"},
        {y: hallRent/(30.5/7), label: "Hall Rent"},
        {y: breakfastCost*7, label: "Breakfast"},
        {y: lunchCost*7, label: "Lunch"},
        {y: dinnerCost*7, label: "Dinner"},
        {y: transportCost*7, label: "Transport Cost"}
      ]

      let monthly = [
        {y: tuitionFee/(5), label: "Tuition Fee"},
        {y: hallRent, label: "Hall Rent"},
        {y: breakfastCost*30.5, label: "Breakfast"},
        {y: lunchCost*30.5, label: "Lunch"},
        {y: dinnerCost*30.5, label: "Dinner"},
        {y: transportCost*30.5, label: "Transport Cost" }
      ]

      let semesterly = [
        {y: tuitionFee, label: "Tuition Fee"},
        {y: hallRent*5, label: "Hall Rent"},
        {y: breakfastCost*30.5*5, label: "Breakfast"},
        {y: lunchCost*30.5*5, label: "Lunch"},
        {y: dinnerCost*30.5*5, label: "Dinner"},
        {y: transportCost*30.5*5, label: "Transport Cost"}
      ]

      return [daily, weekly, monthly, semesterly];
    }
  },
  
  components: {

  },

  firebase: {
    profiles: profilesRef,
    universities: universitiesRef,
    citizenships : citizenshipsRef,
    courses : coursesRef,
    halls: hallsRef,
    meals: mealsRef
  },
}

</script>


<style>
</style>