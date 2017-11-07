<template>
  <div id="app">

    <div id="landing">
      <div class="centered">
        <div class="container">
          <div class="row">
            <h1>PreparedForU</h1>            
          </div>
          <div class="row">
            <div class="col-md-8 col-md-offset-2">
              <p>A simple tool for university aspirants and students in Singapore to estimate and visualize their spending on tuition, rent, transport and living based on publically available data.</p>
            </div>            
          </div>
          <div class="row text-center">
            <div class="col-md-4 col-md-offset-4">
              <div class="col-md-8 col-md-offset-2">
               <a href="#carousel" class="btn btn-start btn-block">Get Started</a>
              </div>
            </div>
          </div>
        </div>
      </div>
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
      <div class="carousel-inner centered">
        
        <div class="item active">
          
          <div class="container" style="margin-top: 0px;">
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
              <div class="col-md-4 col-md-offset-4">
                <select class="form-control" v-model="newProfile.course">
                  <option v-for="course in courses" v-if="course.university==newProfile.university && course.citizenship==newProfile.citizenship" :id="course.course" v-bind:value="course">
                    {{course.course}}
                  </option>
              </select>
              </div>
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

          <div class="container" style="margin-top: 0px;">
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
              <div class="col-md-4 col-md-offset-4">
                <select class="form-control" v-model="newProfile.hall">
                  <option v-for="hall in halls" v-if="hall.university==newProfile.university && newProfile.roomOccupancy==hall.occupancy && newProfile.roomAirCon==hall.airCon" :id="hall.hall" v-bind:value="hall">
                    {{hall.hall}}
                  </option>
                </select>  
              </div>
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

          <div class="container" style="margin-top: 0px;">
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
                <input type="text" id="home" placeholder="Enter Postal Code" v-model="newProfile.home" style="color:#21374B; background-color: #eee;">
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
              <a href="#result" class="col-md-4 col-md-offset-4 btn btn-submit" v-if="newProfile.meal" v-on:click="financialBreakdown=calculateFinancialBreakdown(); show_chart='daily'">Submit</a>
            </div>
          </div>

        </div>

      </div>

      <!-- Left and right controls -->
      <!-- <a class="left carousel-control" href="#carousel" data-slide="prev">
        <span class="glyphicon glyphicon-chevron-left"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="right carousel-control" href="#carousel" data-slide="next">
        <span class="glyphicon glyphicon-chevron-right"></span>
        <span class="sr-only">Next</span>
      </a> -->
    
    </div>
    
    <div id="result" class="container text-center">
      <div class="row">
        <div class="col-md-4">
          <div class="row">
            <div class="col-md-8 col-md-offset-2">
              <select class="form-control" v-model="show_chart">
                <option value="daily">Daily</option>
                <option value="weekly">Weekly</option>
                <option value="monthly">Monthly</option>
                <option value="semesterly">Semesterly</option>
              </select>
            </div>
          </div>
          {{financialBreakdown}}
        </div>
        <div class="col-md-8">
          <bar-chart :legend="true" v-if="show_chart" :data="[{name:newProfile.university, data:financialBreakdown[show_chart]}]" :library="{}"></bar-chart>
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
      show_chart : null
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
      
      let daily = {
        "Tuition Fee" : tuitionFee/(30.5*5),
        "Hall Rent" : hallRent/30.5,
        "Breakfast" : breakfastCost,
        "Lunch" : lunchCost,
        "Dinner" : dinnerCost,
        "Transport Cost" : transportCost
      }

      let weekly = {
        "Tuition Fee" : tuitionFee/(30.5*5/7),
        "Hall Rent" : hallRent/(30.5/7),
        "Breakfast" : breakfastCost*7,
        "Lunch" : lunchCost*7,
        "Dinner" : dinnerCost*7,
        "Transport Cost" : transportCost*7
      }

      let monthly = {
        "Tuition Fee" : tuitionFee/5,
        "Hall Rent" : hallRent,
        "Breakfast" : breakfastCost*30.5,
        "Lunch" : lunchCost*30.5,
        "Dinner" : dinnerCost*30.5,
        "Transport Cost" : transportCost*30.5
      }

      let semesterly = {
        "Tuition Fee" : tuitionFee,
        "Hall Rent" : hallRent*5,
        "Breakfast" : breakfastCost*30.5*5,
        "Lunch" : lunchCost*30.5*5,
        "Dinner" : dinnerCost*30.5*5,
        "Transport Cost" : transportCost*30.5*5
      }

      return {
        'daily' : daily,
        'weekly' : weekly, 
        'monthly' : monthly, 
        'semesterly' : semesterly
      }
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

body {
    font-family: 'Open Sans', 'Helvetica Neue', Arial, sans-serif;
}

#landing {
  background-image: url("assets/header.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  height: 100vh;
}

#carousel {
  height: 100vh; 
  background: #21374B;
}

#result {
  height: 100vh;
}

.carousel-indicators {
  color: #eee;
}

.item {
  text-align: center; 
}

.centered {
  position: absolute;
  left: 50%;
  top: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}

#landing h1 {
  text-align: center;
  font-weight: 400;
  font-stretch: normal;
  font-size: 76px;
  line-height: 80px;
  font-family: Oswald, sans-serif;
  letter-spacing: 1.52px;
  margin-bottom: 40px;
  color: #eee;
}

#landing p {
  text-align: justify; 
  color: #eee; 
  font-weight: 400;
  font-stretch: normal;
  font-size: 16px;
  line-height: 30px;
  font-family: Quattrocento, sans-serif;
  width: 50%;
  margin: 0 auto;
  padding: 30px 0;
  border-bottom: 2px solid #eee;
  border-top: 2px solid #eee;
}

#carousel .container {
  margin-top: 20px;
}

#carousel .form-control {
  color: #21374B; 
  background-color: #eee;
}

#carousel h1 {
  color: #eee;
  font-weight: lighter;
}

#carousel h3 {
  color: #eee;
  font-weight: lighter;
}

#carousel hr {
    max-width: 100px;
    border-width: 3px;
    border-color: #4A89AA;
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

.btn-start {
  margin-top: 50px;
  color: #EDCE06;
  background-color: transparent;
  border-color: #EDCE06;
  border-width: 2px;
  font-weight: bold;
  text-transform: uppercase;
}

.btn-start:hover,
.btn-start:focus,
.btn-start.focus,
.btn-start:active,
.btn-start.active {
  color: #8888888;
  background-color: #EDCE06;
  border-color: #EDCE06;  
}

.btn-option {
  color: #eee;
  background-color: #21374B;
  border-color: #eee;
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
  color: #eee;
  background-color: #21374B;
  border-color: #4A89AA;
  border-width: 2px;
  font-weight: bold;
  text-transform: uppercase;
  margin-top: 20px;
  margin-bottom: 40px;
}

.btn-submit:hover,
.btn-submit:focus,
.btn-submit.focus,
.btn-submit:active,
.btn-submit.active {
  color: #eee;
  background-color: #4A89AA;
  border-color: #4A89AA;
}

</style>