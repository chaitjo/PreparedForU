<template>
  <div id="app">

    <!-- <div class="bg" style="height: 100vh;">
      <h1 style="text-align: center; padding-top: 250px; color: white; ">PreparedForU</h1>
    </div> -->

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
                <h2>Select your university</h2>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div v-for="university in universities">
                <div class="col-md-4"> 
                  <div class="btn btn-option btn-block">
                    <input type="radio" :id="university.fullName" :value="university.value" v-model="newProfile.university">
                    <label :for="university.fullName">{{university.fullName}}</label>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.university">
            <div class="row">
              <h2>What is your citizenship status?</h2>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div v-for="citizenship in citizenships">
                <div class="col-md-4">
                  <div class="btn btn-option btn-block">
                    <input type="radio" :id="citizenship.citizenship" :value="citizenship.value" v-model="newProfile.citizenship">
                    <label :for="citizenship.citizenship">{{citizenship.citizenship}}</label>  
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.citizenship">
            <div class="row">
              <h2>Select your course</h2>
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
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit">Next</a>
            </div>
          </div>
        
        </div>

        <div class="item" v-if="newProfile.course">
          
          <div class="col-md-12" v-if="newProfile.course">
            <div>
              <h2>Will you be staying in on-campus housing?</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="Yes" value="true" v-model="newProfile.stayingOnCampus">
                <label for="Yes">Yes</label>
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="No" value="false" v-model="newProfile.stayingOnCampus">
                <label for="No">No</label>
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.stayingOnCampus=='true'">
            <div>
              <h2>Select your room type</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="Single" value="Single" v-model="newProfile.roomOccupancy">
                <label for="Single">Single Occupancy</label>  
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="Double" value="Double" v-model="newProfile.roomOccupancy">
                <label for="Double">Double Occupancy</label>  
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.roomOccupancy">
            <div>
              <h2>Will your room be equiped with an air conditioner</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="Yes" value="Yes" v-model="newProfile.roomAirCon">
                <label for="Yes">Yes</label>                
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="No" value="No" v-model="newProfile.roomAirCon">
                <label for="No">No</label>  
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.roomAirCon">
            <div>
              <h2>Select your hall</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <select class="col-md-4 col-md-offset-4" v-model="newProfile.hall">
                <option v-for="hall in halls" v-if="hall.university==newProfile.university && newProfile.roomOccupancy==hall.occupancy && newProfile.roomAirCon==hall.airCon" :id="hall.hall" v-bind:value="hall">
                  {{hall.hall}}
                </option>
              </select>
            </div>
          </div>
              
          <div class="col-md-12" style="margin-top: 25px;" v-if="newProfile.stayingOnCampus">
            <a href="#carousel" data-slide="next" class="col-md-2 col-md-offset-5 btn btn-option btn block">Next</a>
          </div>

        </div>

        <div class="item" v-if="newProfile.stayingOnCampus">
          
          <div class="col-md-12" v-if="newProfile.stayingOnCampus=='true'">
            <div>
              <h2>Will you usually be living on-campus during weekends as well?</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="Yes" value="true" v-model="newProfile.stayingOnCampusWeekends">
                <label for="Yes">Yes</label>
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="No" value="false" v-model="newProfile.stayingOnCampusWeekends">
                <label for="No">No</label>
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.stayingOnCampus=='false' || newProfile.stayingOnCampusWeekends=='false'">
            <div>
              <h2>Set your home location</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4">
                <input type="text" id="home" placeholder="Enter Postal Code" v-model="newProfile.home">
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.home">
            <div>
              <h2>What will be your usual mode of transport from home?</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="public" value="public" v-model="newProfile.transport">
                <label for="public">Public Transport</label>  
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="taxi" value="taxi" v-model="newProfile.transport">
                <label for="taxi">Taxi</label>
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="personal" value="personal" v-model="newProfile.transport">
                <label for="personal">Personal Vehicle</label>
              </div>
            </div>
          </div>

          <div class="col-md-12" style="margin-top: 25px;" v-if="newProfile.stayingOnCampusWeekends || newProfile.home">
            <a href="#carousel" data-slide="next" class="col-md-2 col-md-offset-5 btn btn-option btn block">Next</a>
          </div>

        </div>

        <div class="item" v-if="newProfile.stayingOnCampusWeekends || newProfile.home">

          <div class="col-md-12">
            <div class="col-md-8 col-md-offset-2">
              <h2>Select your dietary preference</h2>
            </div>
            <div class="col-md-8 col-md-offset-2" v-for="meal in meals" v-if="meal.university==newProfile.university">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" :id="meal.diet" :value="meal" v-model="newProfile.meal">
                <label :for="meal.diet">{{meal.diet}}</label>
              </div>
            </div>
          </div>

          <div class="col-md-12" v-if="newProfile.meal && newProfile.home">
            <div>
              <h2>Will you usually be having breakfast/dinner on campus or at home?</h2>
            </div>
            <div class="col-md-8 col-md-offset-2">
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="campus" value="false" v-model="newProfile.foodAtHome">
                <label for="campus">On campus</label>  
              </div>
              <div class="col-md-4 col-md-offset-4 btn btn-option">
                <input type="radio" id="home" value="true" v-model="newProfile.foodAtHome">
                <label for="nonveg">At home</label>
              </div>
            </div>
          </div>
          
          <div class="col-md-12" style="margin-top: 25px;" v-if="newProfile.meal">
            <a href="#result" class="col-md-2 col-md-offset-5 btn btn-option" v-if="newProfile.meal" v-on:click="myGovDataAPI('e1c20915-ab7c-4bf9-bbbd-0197bbc7b98c'); createChart('daily', financialBreakdown[0]); createChart('weekly', financialBreakdown[1]); createChart('monthly', financialBreakdown[2]); createChart('semesterly', financialBreakdown[3])">Submit</a>
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
    
    <div id="result" class="col-md-12 text-center">
      <div id="daily" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="weekly" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="monthly" style="height: 500px; width: 100%;"></div>
      <hr>
      <div id="semesterly" style="height: 500px; width: 100%;"></div>
    </div>

    <div class="col-md-12 text-center" style="margin-top: 50px;">
      {{newProfile}}
      <hr>
      {{financialBreakdown}}
      <hr>
      {{temp_data}}
      <hr>
      {{show_chart}}
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
      show_chart : false
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
      this.show_chart = true;
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
      console.log(plotData);
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

.bg { 
    background-image: url("assets/header.jpg");
    height: 100%; 
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}

[type='radio'] {
  visibility:hidden;
}

label {
  cursor: pointer;
  font-weight: normal;
  text-align: center;
  padding-right: 15px;
}

.carousel {
  height: 100vh; 
  background: #21374B;
}

.item {
  text-align: center; 
  margin-top: 100px;
}

.container {
  margin-top: 20px;
}

h2 {
  color: #E7DACB;
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
  border-width: 1px;
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
  background-color: #E7DACB;
}

</style>