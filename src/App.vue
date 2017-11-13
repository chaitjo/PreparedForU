<template>
  <div id="app" v-smoothscroll="{ duration : 500, callback: callback , context : undefined }">

    <div id="landing">
      <div class="centered">
        <div class="container">
          <div class="row">
            <h1>PreparedFor<span style="color: #FF8C00; font-weight: 500;">U</span></h1>            
          </div>
          <div class="row">
            <div class="col-md-8 col-md-offset-2">
              <p>A simple tool for university aspirants and students in Singapore to estimate and visualize their spending on tuition, rent, transport and living based on publicaly available data.</p>
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
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit" v-on:click="myOneMapSearchAPI(newProfile.university, 'university');">Next</a>
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

          <div class="container" v-if="newProfile.stayingOnCampus=='true' && newProfile.roomOccupancy">
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

          <div class="container" v-if="newProfile.stayingOnCampus=='true' && newProfile.roomAirCon">
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
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit" v-on:click="myGovDataAPI('70f568d2-85a4-4926-ab7a-e28c7728b6c0','Train'); myGovDataAPI('e1c20915-ab7c-4bf9-bbbd-0197bbc7b98c', 'Bus'); myGovDataAPI('a9e3c103-8310-41c0-abbf-c4e1adb35aa4', 'Concession');">Next</a>
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
                <input type="text" id="home" placeholder="Enter Postal Code" v-model="newProfile.home" style="margin-top: 4px; color:#21374B; background-color: #eee;">
              </div>
              <div class="col-md-2">
                <a href="#carousel" class="btn btn-submit btn-block" style="margin-left: -55px; margin-top: 0px; margin-bottom: 0px;" v-on:click="myOneMapSearchAPI(newProfile.home, 'home');">Set</a>
              </div>
            </div>
          </div>

          <div class="container" v-if="(newProfile.stayingOnCampusWeekends=='false' || !(newProfile.stayingOnCampusWeekends)) && newProfile.homeLatLong">
            <div class="row">
              <h3>What will be your usual mode of transport from home?</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4 col-md-offset-2">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.transport=='public'}">
                  <input type="radio" id="public" value="public" v-model="newProfile.transport">
                  <label for="public">Public Transport</label>  
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

          <div class="container" v-if="(newProfile.stayingOnCampusWeekends=='false' || !(newProfile.stayingOnCampusWeekends)) && newProfile.home && newProfile.transport=='public'">
            <div class="row">
              <h3>Select your concession card type</h3>
            </div>
            <div class="row col-md-10 col-md-offset-1">
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.concession=='bus'}">
                  <input type="radio" id="bus" value="bus" v-model="newProfile.concession">
                  <label for="bus">Bus Only</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.concession=='train'}">
                  <input type="radio" id="train" value="train" v-model="newProfile.concession">
                  <label for="train">Train Only</label>
                </div>
              </div>
              <div class="col-md-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.concession=='hybrid'}">
                  <input type="radio" id="hybrid" value="hybrid" v-model="newProfile.concession">
                  <label for="hybrid">Hybrid</label>
                </div>
              </div>
            </div>
            <div class="row col-md-10 col-md-offset-1" style="margin-top: 10px;">
              <div class="col-md-4 col-md-offset-4">
                <div class="col-md-12 btn btn-option" v-bind:class="{active: newProfile.concession=='none'}">
                  <input type="radio" id="none" value="none" v-model="newProfile.concession">
                  <label for="none">None</label>
                </div>
              </div>
            </div>
          </div>

          <div class="container" v-if="newProfile.stayingOnCampus=='true' && newProfile.stayingOnCampusWeekends=='true' || (newProfile.transport=='public' && newProfile.concession) || newProfile.transport=='taxi' || newProfile.transport=='personal'">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#carousel" data-slide="next" class="col-md-4 col-md-offset-4 btn btn-submit" v-on:click="myOneMapRouteAPI();">Next</a>
            </div>
          </div>

        </div>

        <div class="item" v-if="(show_restart=='true') || (newProfile.stayingOnCampusWeekends || newProfile.home)">

          <div class="container" v-if="show_restart=='false'">
            <div class="row">
              <h1>Food</h1>
              <hr>
            </div>
          </div>

          <div class="container" v-if="show_restart=='false'" style="margin-top: 0px;">
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

          <div class="container" v-if="newProfile.meal && newProfile.home && newProfile.stayingOnCampus=='false'">
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
          
          <div class="container" v-if="(newProfile.home && newProfile.foodAtHome) || (newProfile.stayingOnCampusWeekends=='false' && newProfile.meal) || (newProfile.home==null && newProfile.meal)">
            <div class="row col-md-10 col-md-offset-1">
              <hr>
              <a href="#result" class="col-md-4 col-md-offset-4 btn btn-submit" v-if="newProfile.meal" v-on:click="show_chart='0'; myOneMapRouteAPI(); calculateFinancialBreakdown();">Submit</a>
            </div>
          </div>

          <div class="container" v-if="show_restart=='true'">
            <div class="row col-md-4 col-md-offset-4">
              <a href="#carousel" data-slide="next" class="col-md-8 col-md-offset-2 btn btn-start" v-on:click="show_restart='false';">Re-enter Responses</a>
            </div>
          </div>

        </div>

      </div>

      <!-- Left and right controls -->
      <!-- <div v-if="show_compare">
        <a class="left carousel-control" href="#carousel" data-slide="prev">
          <span class="glyphicon glyphicon-chevron-left"></span>
          <span class="sr-only">Previous</span>
        </a>
        <a class="right carousel-control" href="#carousel" data-slide="next">
          <span class="glyphicon glyphicon-chevron-right"></span>
          <span class="sr-only">Next</span>
        </a>
      </div> -->
    
    </div>
    
    <div id="result"> 
      <div class="container text-center" v-if="show_chart"> 
        <div class="row">
          <div class="col-md-3 col-md-offset-1">
              <select class="form-control" v-model="show_chart">
                <option value="0" selected>Daily</option>
                <option value="1">Weekly</option>
                <option value="2">Monthly</option>
                <option value="3">Semesterly</option>
              </select>
          </div>
          <h1 v-if="!(show_compare)">, You'll be spending S$ <span style="color: #3366cc; font-weight: 700">{{totalSpending[show_chart].toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span></h1>
          <h1 v-if="show_compare">, You'll be spending S$ <span style="color: #3366cc; font-weight: 700;">{{totalSpending[show_chart].toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span> vs <span style="color: #dc3912; font-weight: 700">{{oldTotalSpending[show_chart].toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")}}</span></h1>
        </div>
        <div class="row">
          <div class="col-md-10 col-md-offset-1">
            <bar-chart :legend="true" legend="bottom" v-if="show_chart && !(show_compare)" :data="[financialBreakdown[show_chart]]"></bar-chart>
            <bar-chart :legend="true" legend="bottom" v-else-if="show_chart && show_compare" :data="[financialBreakdown[show_chart], oldFinancialBreakdown[show_chart]]"></bar-chart>
          </div>
        </div>
        <div class="row col-md-4 col-md-offset-4">
          <a href="#carousel" class="btn btn-compare col-md-8 col-md-offset-2" v-on:click="compareProfiles()">Compare</a>
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
          universityLatLong : null,
          citizenship : null,
          course : null,
          stayingOnCampus : null,
          stayingOnCampusWeekends : null,
          roomOccupancy : null,
          roomAirCon : null,
          hall : null,
          home : null,
          homeLatLong : null,
          concession : null,
          meal : null,
          foodAtHome : null,
          transport : null,
          route : null,
      },
      temp_data : null,
      concessionData : null,
      faresTrainData : null,
      faresBusData : null,
      totalSpending : [],
      oldTotalSpending : null,
      financialBreakdown : null,
      oldFinancialBreakdown : null,
      show_chart : null,
      show_compare : null,
      show_restart : 'false',
    }
  },

  methods: {

    myGovDataAPI: function (resource_id, modifier) {
      let url = "https://data.gov.sg/api/action/datastore_search?resource_id=" + resource_id;
      console.log(url);
      axios.get(url).then((response) => {
        if (modifier=='Train') {
          this.faresTrainData = response.data.result.records;
        }
        else if (modifier=='Bus') {
          this.faresBusData = response.data.result.records;
        }
        else if (modifier=='Concession') {
          this.concessionData = response.data.result.records[3];
        }
        else {
          this.temp_data = response.data;
        }
      }).catch( error => { console.log(error); });
    },

    myOneMapSearchAPI: function (searchText, modifier) {
      let url = "https://developers.onemap.sg/commonapi/search?searchVal=" + searchText + "&returnGeom=Y&getAddrDetails=N&pageNum=1";
      console.log(url);
      axios.get(url).then((response) => {
        if (modifier=='university') {
          this.newProfile.universityLatLong = response.data.results[0].LATITUDE + ',' + response.data.results[0].LONGITUDE;
        }
        else if (modifier=='home') {
          this.newProfile.homeLatLong = response.data.results[0].LATITUDE + ',' + response.data.results[0].LONGITUDE;
        } 
        else {
          this.temp_data = response.data;
        }
      }).catch( error => { console.log(error); });
    },

    myOneMapRouteAPI: function () {
      let start = this.newProfile.homeLatLong;
      let end = this.newProfile.universityLatLong;
      let routeType = 'pt';
      let token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEwODMsInVzZXJfaWQiOjEwODMsImVtYWlsIjoiY2tqb3NoaTlAZ21haWwuY29tIiwiZm9yZXZlciI6ZmFsc2UsImlzcyI6Imh0dHA6XC9cL29tMi5kZmUub25lbWFwLnNnXC9hcGlcL3YyXC91c2VyXC9zZXNzaW9uIiwiaWF0IjoxNTEwNTM4MDk3LCJleHAiOjE1MTA5NzAwOTcsIm5iZiI6MTUxMDUzODA5NywianRpIjoiNGUwNzkzMzk0ZTE5NzIwM2M1NTFhMDE4MTM0ZGU4NDUifQ.W3vFyZwylJLOFzohfCpOBEAqjLM0jCRJ7E30gAtdeow';
      let date = '2017-11-07';
      let time = '10:00:00';
      let mode = 'TRANSIT';
      let url = "https://developers.onemap.sg/privateapi/routingsvc/route?" + "start=" + start + "&end=" + end + "&routeType=" + routeType + "&token=" + token + "&date=" + date + "&time=" + time + "&mode=" + mode + "&numItineraries=1";
      console.log(url)
      axios.get(url).then((response) => {
        this.newProfile.route = response.data.plan.itineraries[0];
        }).catch( error => { console.log(error); });
    },

    calculateFinancialBreakdown: function() {
      this.totalSpending = [];

      let tuitionFee = [0, 0, 0, 0];
      if (this.newProfile.course!=null) {
        tuitionFee[3] = Number(this.newProfile.course.fee)/2;
        tuitionFee[0] = tuitionFee[3]/(30.5*5);
        tuitionFee[1] = tuitionFee[3]/((30.5*5/7));
        tuitionFee[2] = tuitionFee[3]/5;
      }

      let hallRent = [0, 0, 0, 0];
      if (this.newProfile.hall!=null) {
        hallRent[2] = Number(this.newProfile.hall.rent);
        hallRent[0] = hallRent[2]/30.5;
        hallRent[1] = hallRent[2]/(30.5/7);
        hallRent[3] = hallRent[2]*5;
      }

      let transportCost = [0,0,0,0];
      let concessionCost = [0,0,0,0];
      if (this.newProfile.home && this.newProfile.transport=='public') { 
        if (this.newProfile.concession!='none') {
          concessionCost[2] = Number(this.concessionData[this.newProfile.concession+'_price']);
          concessionCost[3] = concessionCost[2]*5;
        }
          
        let dist_bus = 0;
        let dist_train = 0;
        for (let i=0; i<this.newProfile.route.legs.length; i++) {
          if(this.newProfile.route.legs[i].mode == "BUS"){
            dist_bus += this.newProfile.route.legs[i].distance;
          }
          if(this.newProfile.route.legs[i].mode == "SUBWAY") {
            dist_train += this.newProfile.route.legs[i].distance;
          }
        }

        console.log(dist_bus, dist_train)
        
        let trainCost = 0;
        if(dist_train>0) {
          dist_train /= 1000;
          if (dist_train <= 3.2) {
            console.log(dist_train, "is less than 3.2")
            if (this.newProfile.concession=='train' || this.newProfile.concession=='hybrid') {
              trainCost = 0;
            }
            else {
              trainCost = Number(this.faresTrainData[0]["adult_card_fare_per_ride"]);
            }
          }
          else if (dist_train > 40.2) {
            console.log(dist_train, "is greater that 40.2")
            if (this.newProfile.concession=='train' || this.newProfile.concession=='hybrid') {
              trainCost = 0;
            }
            else {
              trainCost = Number(this.faresTrainData[this.faresTrainData.length-1]["adult_card_fare_per_ride"]);
            }
          }
          else {
            for (let i=1; i<this.faresTrainData.length-1; i++) {
              let start = Number(this.faresTrainData[i]['distance'].slice(0, this.faresTrainData[i]['distance'].indexOf('-')).replace(/[^0-9\.]+/g,""));
              let end = Number(this.faresTrainData[i]['distance'].slice(this.faresTrainData[i]['distance'].indexOf('-')).replace(/[^0-9\.]+/g,""));
              if (start <= dist_train && dist_train <= end) {
                if (this.newProfile.concession=='train' || this.newProfile.concession=='hybrid') {
                  trainCost = 0;
                }
                else {
                  trainCost = Number(this.faresTrainData[i]["adult_card_fare_per_ride"]);
                }
                break;
              }
            }
          }
        }

        let busCost = 0;
        if(dist_bus>0){
          dist_bus /= 1000;
          if (0 < dist_bus <= 3.2) {
            if (this.newProfile.concession=='bus' || this.newProfile.concession=='hybrid') {
              busCost = 0;
            }
            else {
              busCost = Number(this.faresBusData[0]["adult_card_fare_per_ride"]);
            }
          }
          else if (dist_bus > 40.2) {
           if (this.newProfile.concession=='bus' || this.newProfile.concession=='hybrid') {
              busCost = 0;
            }
            else {
              busCost = Number(this.faresBusData[this.faresBusData.length-1]["adult_card_fare_per_ride"]);
            } 
          }
          else {
            for (let i=0; i<this.faresBusData.length; i++) {
              let start = Number(this.faresBusData[i]['distance'].slice(0, this.faresBusData[i]['distance'].indexOf('-')).replace(/[^0-9\.]+/g,""));
              let end = Number(this.faresBusData[i]['distance'].slice(this.faresBusData[i]['distance'].indexOf('-')).replace(/[^0-9\.]+/g,""));
              if (start <= dist_bus && dist_bus <= end) {
                if (this.newProfile.concession=='bus' || this.newProfile.concession=='hybrid') {
                  busCost = 0;
                }
                else {
                  busCost = Number(this.faresBusData[i]["adult_card_fare_per_ride"]);
                }
                break;
              }
            }
          }
        }

        if (this.newProfile.stayingOnCampus=='false') {
          transportCost[0] = (busCost/100 + trainCost/100)*2;
          transportCost[1] = transportCost[0]*5;
        }
        else if (this.newProfile.stayingOnCampusWeekends=='false') {
          transportCost[0] = 0;
          transportCost[1] = (busCost/100 + trainCost/100)*2;
        }
        transportCost[2] = transportCost[1]*(30.5/7);
        transportCost[3] = transportCost[2]*5;
      }

      let breakfastCost = [0,0,0,0];
      if (this.newProfile.meal!=null && !(this.newProfile.home && this.newProfile.foodAtHome=='true')) {
        breakfastCost[0] = Number(this.newProfile.meal.breakfast);
        if (this.newProfile.stayingOnCampusWeekends=='false' || this.newProfile.stayingOnCampus=='false') {
          breakfastCost[1] = breakfastCost[0]*5;
        }
        else {
          breakfastCost[1] = breakfastCost[0]*7;
        }
        breakfastCost[2] = breakfastCost[1]*(30.5/7);
        breakfastCost[3] = breakfastCost[2]*5;
      }
      
      let lunchCost = [0,0,0,0];
      if (this.newProfile.meal!=null) {
        lunchCost[0] = Number(this.newProfile.meal.lunch);
        if (this.newProfile.stayingOnCampusWeekends=='false' || this.newProfile.stayingOnCampus=='false') {
          lunchCost[1] = lunchCost[0]*5;
        }
        else {
          lunchCost[1] = lunchCost[0]*7;
        }
        lunchCost[2] = lunchCost[1]*(30.5/7);
        lunchCost[3] = lunchCost[2]*5;
      }

      let dinnerCost = [0,0,0,0];
      if (this.newProfile.meal!=null && !(this.newProfile.home && this.newProfile.foodAtHome=='true')) {
        dinnerCost[0] = Number(this.newProfile.meal.dinner);
        if (this.newProfile.stayingOnCampusWeekends=='false' || this.newProfile.stayingOnCampus=='false') {
          dinnerCost[1] = dinnerCost[0]*5;
        }
        else {
          dinnerCost[1] = dinnerCost[0]*7;
        }
        dinnerCost[2] = dinnerCost[1]*(30.5/7);
        dinnerCost[3] = dinnerCost[2]*5;
      }
      
      this.financialBreakdown = []
      for (let i=0; i<4; i++) {
        if (i<2) {
          this.financialBreakdown[i] = {
            name : this.newProfile.university,
            data : {
              //"Tuition Fee" : tuitionFee[i],
              //"Hall Rent" : hallRent[i],
              "Transport Cost" : transportCost[i],
              "Breakfast" : breakfastCost[i],
              "Lunch" : lunchCost[i],
              "Dinner" : dinnerCost[i]
            }
          }
        }

        else if (i==2) {
          this.financialBreakdown[i] = {
            name : this.newProfile.university,
            data : {
              // "Tuition Fee" : tuitionFee[i],
              "Hall Rent" : hallRent[i],
              "Transport Cost" : transportCost[i],
              "Concession Cost" : concessionCost[i],
              "Breakfast" : breakfastCost[i],
              "Lunch" : lunchCost[i],
              "Dinner" : dinnerCost[i]
            }
          }  
        }

        else if (i==3) {
          this.financialBreakdown[i] = {
            name : this.newProfile.university,
            data : {
              "Tuition Fee" : tuitionFee[i],
              "Hall Rent" : hallRent[i],
              "Transport Cost" : transportCost[i],
              "Concession Cost" : concessionCost[i],
              "Breakfast" : breakfastCost[i],
              "Lunch" : lunchCost[i],
              "Dinner" : dinnerCost[i]
            }
          }  
        }

        this.totalSpending[i] = 0;
        for (var key in this.financialBreakdown[i]["data"]) {
          this.totalSpending[i] += this.financialBreakdown[i]["data"][key];
        } 
      }
    },

    compareProfiles: function() {
      this.newProfile = {};
      this.oldFinancialBreakdown = this.financialBreakdown;
      this.oldTotalSpending = this.totalSpending; 
      this.show_compare = 'true';
      this.show_restart = 'true';
    }
  },

  computed: {
  
  },
  
  components: {

  },

  firebase: {
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
  font-weight: 300;
  font-stretch: normal;
  font-size: 76px;
  line-height: 80px;
  font-family: Oswald, sans-serif;
  letter-spacing: 2px;
  margin-bottom: 40px;
  color: #eee;
}

#landing p {
  text-align: justify; 
  color: #eee; 
  font-weight: 400;
  font-stretch: normal;
  font-size: 16px;
  line-height: 24px;
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
  font-family: Quattrocento, sans-serif;
  font-weight: 400;
  font-size: 42px;
  color: #eee;
}

#carousel h3 {
  color: #eee;
  font-size: 20px;
  font-weight: lighter;
}

#carousel hr {
    max-width: 100px;
    border-width: 3px;
    border-color: #4A89AA;
}

select {
  text-align-last:center;
}

#result select {
  margin-top: 9px; 
  font-size: 36px; 
  height: 65px; 
}

#result h1 {
  text-align: left;
}

#result .row {
  margin-top: 50px;
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
  color: #FF8C00;
  background-color: transparent;
  border-color: #FF8C00;
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
  background-color: #FF8C00;
  border-color: #FF8C00;  
}

.btn-option {
  color: #eee;
  background-color: transparent;
  border-color: #eee;
}

.btn-option:hover,
.btn-option:focus,
.btn-option.focus,
.btn-option:active,
.btn-option.active {
  color: #21374B;
  background-color: #FF8C00;
  border-color: #FF8C00;  
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

.btn-compare {
  color: #21374B;
  background-color: transparent;
  border-color: #21374B;
  border-width: 2px;
  font-weight: bold;
  text-transform: uppercase;
}

.btn-compare:hover,
.btn-compare:focus,
.btn-compare.focus,
.btn-compare:active,
.btn-compare.active {
  color: #fff;
  background-color: #21374B;
  border-color: #21374B;  
}

</style>