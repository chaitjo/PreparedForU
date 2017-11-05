<template>
  <div id="app">

    <div class="bg" style="height: 100vh;">
      <h1 style="text-align: center; padding-top: 250px; color: white; ">PreparedForU</h1>
    </div>

    <div id="carousel" class="carousel slide" data-ride="carousel" data-interval="false">
      <!-- Indicators -->
      <ol class="carousel-indicators">
        <li data-target="#carousel" data-slide-to="0" class="active"></li>
        <li data-target="#carousel" data-slide-to="1"></li>
        <li data-target="#carousel" data-slide-to="2"></li>
        <li data-target="#carousel" data-slide-to="3"></li>
      </ol>

      <!-- Wrapper for slides -->
      <div class="carousel-inner">
        
        <div class="item active">
          
          <div class="container">
            <div class="row">
              <h1>Tuition</h1>
              <hr>
            </div>
          </div>

          <div class="container" style="margin-top: 0px;">
            <div class="row">
                <h3>Select your university</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div v-for="university in universities">
                <div class="col-md-4"> 
                  <div class="btn btn-option btn-block" v-bind:class="{active: university.value==newProfile.university}">
                    <input type="radio" :id="university.fullName" :value="university.value" v-model="newProfile.university">
                    <label :for="university.fullName">{{university.fullName}}</label>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.university">
            <div class="row">
              <h3>What is your citizenship status?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div v-for="citizenship in citizenships">
                <div class="col-md-4">
                  <div class="btn btn-option btn-block" v-bind:class="{active: citizenship.value==newProfile.citizenship}">
                    <input type="radio" :id="citizenship.citizenship" :value="citizenship.value" v-model="newProfile.citizenship">
                    <label :for="citizenship.citizenship">{{citizenship.citizenship}}</label>  
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.citizenship">
            <div class="row">
              <h3>Select your course</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <select class="col-md-4 col-md-offset-4" v-model="newProfile.course">
                <option v-for="course in courses" v-if="course.university==newProfile.university && course.citizenship==newProfile.citizenship" :id="course.course" v-bind:value="course">
                  {{course.course}}
                </option>
              </select>
            </div>
          </div>

          <div class="container" v-if="newProfile.course">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit">Next</a>
            </div>
          </div>
        
        </div>

        <div class="item" v-if="newProfile.course">

          <div class="container">
            <div class="row">
              <h1>Housing and Rent</h1>
              <hr>
            </div>
          </div>
          
          <div class="container" v-if="newProfile.course" style="margin-top: 0px;">
            <div class="row">
              <h3>Will you be staying in on-campus housing?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2"> 
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.stayingOnCampus=='true'}">
                  <input type="radio" id="onCampusYes" value="true" v-model="newProfile.stayingOnCampus">
                  <label for="onCampusYes">Yes</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.stayingOnCampus=='false'}">
                  <input type="radio" id="onCampusNo" value="false" v-model="newProfile.stayingOnCampus">
                  <label for="onCampusNo">No</label>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.stayingOnCampus=='true'">
            <div class="row">
              <h3>Select your room type</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.roomOccupancy=='Single'}">
                  <input type="radio" id="Single" value="Single" v-model="newProfile.roomOccupancy">
                  <label for="Single">Single Occupancy</label>  
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.roomOccupancy=='Double'}">
                  <input type="radio" id="Double" value="Double" v-model="newProfile.roomOccupancy">
                  <label for="Double">Double Occupancy</label>  
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.roomOccupancy">
            <div class="row">
              <h3>Will your room be equiped with an air conditioner</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.roomAirCon=='Yes'}">
                  <input type="radio" id="airConYes" value="Yes" v-model="newProfile.roomAirCon">
                  <label for="airConYes">Yes</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.roomAirCon=='No'}">
                  <input type="radio" id="airConNo" value="No" v-model="newProfile.roomAirCon">
                  <label for="airConNo">No</label>  
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.roomAirCon">
            <div class="row">
              <h3>Select your hall</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <select class="col-md-4 col-md-offset-4" v-model="newProfile.hall">
                <option v-for="hall in halls" v-if="hall.university==newProfile.university && newProfile.roomOccupancy==hall.occupancy && newProfile.roomAirCon==hall.airCon" :id="hall.hall" v-bind:value="hall">
                  {{hall.hall}}
                </option>
              </select>
            </div>
          </div>
          
          <div class="container" v-if="newProfile.stayingOnCampus=='false' || newProfile.hall">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit">Next</a>
            </div>
          </div>

        </div>

        <div class="item" v-if="newProfile.stayingOnCampus">

          <div class="container">
            <div class="row">
              <h1>Transportation</h1>
              <hr>
            </div>
          </div>
          
          <div class="container" v-if="newProfile.stayingOnCampus=='true'" style="margin-top: 0px;">
            <div class="row">
              <h3>Will you usually be living on-campus during weekends as well?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.stayingOnCampusWeekends=='true'}">
                  <input type="radio" id="onWeekendsYes" value="true" v-model="newProfile.stayingOnCampusWeekends">
                  <label for="onWeekendsYes">Yes</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.stayingOnCampusWeekends=='false'}">
                  <input type="radio" id="onWeekendsNo" value="false" v-model="newProfile.stayingOnCampusWeekends">
                  <label for="onWeekendsNo">No</label>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.stayingOnCampus=='false' || newProfile.stayingOnCampusWeekends=='false'">
            <div class="row">
              <h3>Set your home location</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-4">
                <input type="text" id="home" placeholder="Enter Postal Code" v-model="newProfile.home" style="color:#21374B; background-color: #E7DACB;">
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.home">
            <div class="row">
              <h3>What will be your usual mode of transport from home?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.transport=='public'}">
                  <input type="radio" id="public" value="public" v-model="newProfile.transport">
                  <label for="public">Public Transport</label>  
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.transport=='taxi'}">
                  <input type="radio" id="taxi" value="taxi" v-model="newProfile.transport">
                  <label for="taxi">Taxi</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.transport=='personal'}">
                  <input type="radio" id="personal" value="personal" v-model="newProfile.transport">
                  <label for="personal">Personal Vehicle</label>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.stayingOnCampusWeekends=='true' || newProfile.transport">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit">Next</a>
            </div>
          </div>

        </div>

        <div class="item" v-if="newProfile.stayingOnCampusWeekends || newProfile.home">

          <div class="container">
            <div class="row">
              <h1>Food</h1>
              <hr>
            </div>
          </div>

          <div class="container" style="margin-top: 0px;">
            <div class="row">
              <h3>Select your dietary preference</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-2"></div>
              <div v-for="meal in meals" v-if="meal.university==newProfile.university">
                <div class="col-md-4">
                  <div class="col-md-12 btn btn-option" v-bind:class="{active: meal==newProfile.meal}">
                    <input type="radio" :id="meal.diet" :value="meal" v-model="newProfile.meal">
                    <label :for="meal.diet">{{meal.diet}}</label>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.meal && newProfile.home">
            <div class="row">
              <h3>Will you usually be having breakfast/dinner on campus or at home?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.foodAtHome=='false'}">
                  <input type="radio" id="foodCampus" value="false" v-model="newProfile.foodAtHome">
                  <label for="foodCampus">On campus</label>  
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.foodAtHome=='true'}">
                  <input type="radio" id="foodHome" value="true" v-model="newProfile.foodAtHome">
                  <label for="foodHome">At home</label>
                </div>
              </div>
            </div>
          </div>
          
          <div class="container" v-if="newProfile.meal">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#result" class="col-md-4 col-md-offset-4 btn btn-submit" v-if="newProfile.meal" v-on:click="financialBreakdown=calculateFinancialBreakdown(); createChart(show_chart, financialBreakdown[show_chart]);">Submit</a>
            </div>
          </div>

        </div>

      </div>

      <!-- Left and right controls -->
      <a class="left carousel-control" href="#carousel" data-slide="prev">
        <span class="glyphicon glyphicon-chevron-left"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="right carousel-control" href="#carousel" data-slide="next">
        <span class="glyphicon glyphicon-chevron-right"></span>
        <span class="sr-only">Next</span>
      </a>
    
    </div>
    
    <div id="result" class="container text-center">
      <div class="row">
        <div class="col-md-4">
          <div class="row">
            <select v-model="show_chart">
              <option value="daily" selected>Daily</option>
              <option value="weekly" selected>Weekly</option>
              <option value="monthly" selected>Monthly</option>
              <option value="semesterly" selected>Semesterly</option>
            </select>
          </div>
          <div class="row"> 
            <button v-on:click="createChart(show_chart, financialBreakdown[show_chart])">Submit</button>
          </div>
          {{financialBreakdown}}
        </div>
        <div class="col-md-8">
          <div id="daily" v-if="show_chart=='daily'" style="height: 100vh; width: 100%;"></div>
          <div id="weekly" v-if="show_chart=='weekly'" style="height: 100vh; width: 100%;"></div>
          <div id="monthly" v-if="show_chart=='monthly'" style="height: 100vh; width: 100%;"></div>
          <div id="semesterly" v-if="show_chart=='semesterly'" style="height: 100vh; width: 100%;"></div>
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
      temp_data : null,
      financialBreakdown : null,
      show_chart : 'daily'
    }
  },

  methods: {

    myGovDataAPI: function (resource_id) {
      let url = "https://data.gov.sg/api/action/datastore_search?resource_id=" + resource_id;
      axios.get(url).then((response) => {
        this.temp_data = response.data.result.records;
      }).catch( error => { console.log(error); });
    },

    calculateFinancialBreakdown: function() {
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

      return {
        'daily' : daily,
        'weekly' : weekly, 
        'monthly' : monthly, 
        'semesterly' : semesterly
      }
    },

    createChart: function (id, plotData) {
      this.show_chart = id;
      var chart = new CanvasJS.Chart(id, {
        animationEnabled: true,
        title:{
          text: "",
          horizontalAlign: "center"
        },
        data: [{
          type: "doughnut",
          startAngle: 60,
          indexLabelFontSize: 17,
          indexLabel: "{label} - {y}",
          toolTipContent: "<b>{label}:</b> {y} (#percent%)",
          dataPoints: plotData
        }]
      });
      chart.render();
    }
  },

  computed: {
  
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

.bg { 
    background-image: url("assets/header.jpg");
    height: 100%; 
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}

[type='radio'] {
  visibility: hidden;
  width: 0;
  height: 0;
}

label {
  cursor: pointer;
  font-weight: normal;
  text-align: center;
  width: 100%;
  text-align: center;
  margin-bottom: 0;
}

.carousel {
  height: 100vh; 
  background: #21374B;
}

.carousel-indicators {
  color: #E7DACB;
}

.item {
  text-align: center; 
  margin-top: 50px;
}

.container {
  margin-top: 20px;
}

h1 {
  color: #E7DACB;
  font-weight: lighter;
}

h3 {
  color: #E7DACB;
  font-weight: lighter;
}

hr {
    max-width: 100px;
    border-width: 3px;
    border-color: #4A89AA;
}

.btn-option {
  color: #E7DACB;
  background-color: #21374B;
  border-color: #E7DACB;
}

.btn-option:hover,
.btn-option:focus,
.btn-option.focus,
.btn-option:active,
.btn-option.active {
  color: #21374B;
  background-color: #EDCE06;
  border-color: #EDCE06;  
}

.btn-submit {
  color: #E7DACB;
  background-color: #21374B;
  border-color: #4A89AA;
  border-width: 2px;
  font-weight: bold;
  text-transform: uppercase;
  margin-top: 20px;
}

.btn-submit:hover,
.btn-submit:focus,
.btn-submit.focus,
.btn-submit:active,
.btn-submit.active {
  color: #E7DACB;
  background-color: #4A89AA;
  border-color: #4A89AA;
}

select {
  color: #21374B; 
  background-color: #E7DACB;
}

</style>