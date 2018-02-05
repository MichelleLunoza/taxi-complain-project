<template>
  <q-layout>
  <div slot="header">
  <q-toolbar color="warning">
  <q-toolbar-title>{{TaxiReport}}</q-toolbar-title>
  </q-toolbar>

  <q-tabs color="warning">
  <q-route-tab
    icon="local taxi"
    to="/feed"
    @click="feedTab"
    exact
    slot="title"
    label="report feed"    
    name="tab-1"
  />
    <q-route-tab
    icon="report problem"
    to="/report"
    exact
    slot="title"  
    label="report"   
    name="tab-2"  
  />
  </q-tabs>
  </div>
<!-- Report Tab -->
<div class="data-report">
    <div>
    <q-item label>Plate Number:</q-item>
    <q-input v-model="newReport.plate_number" color="warning"/>
    <q-item label>Date of Incident:</q-item>
    <q-datetime v-model="newReport.date" type="date" format="MMMM D,YYYY" color="warning"/>
    <q-item label>Taxi's Name:</q-item>
    <q-input v-model="newReport.taxi_name" placeholder="ex. GRAB Taxi" color="warning"/>
    <q-item label>Details:</q-item>
    <q-input class="textarea"
    v-model="newReport.details"
    type="textarea" color="warning"
    />
    
    <q-list>
    <q-item class="violation-list"label>Violations:</q-item>
     <q-checkbox v-model="selection" val="Refused boarding" label="Refused boarding"color="warning" />
    <br/>
     <q-checkbox v-model="selection" val="Choosing passengers" label="Choosing passengers" color="warning" />
    <br/>
     <q-checkbox v-model="selection" val="Over charging" label="Over charging" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="No meter" label="No meter" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Tampered or broken meter" label="Tampered or broken meter" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Contracting" label="Contracting" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="No receipt" label="No receipt" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Reckless driving" label="Reckless driving" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Rude behavior" label="Rude behavior" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Smoking while driving" label="Smoking while driving" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Not in uniform" label="Not in uniform" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="No seatbelts" label="No seatbelts" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Smelly interiors" label="Smelly interiors" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Dirty seats and interiors" label="Dirty seats and interiors" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Left behind items" label="Left behind items" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Physical assault" label="Physical assault" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Verbal harrassment" label="Verbal harrassment" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Malicious mischief" label="Malicious mischief" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Sexual assault" label="Sexual assault" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Dilapidated" label="Dilapidated" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="No taxi details inside" label="No taxi details inside" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="LPG smells" label="LPG smells" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Texting while driving" label="Texting while driving" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="Not giving exact change" label="Not giving exact change" color="warning"/>
    <br/>
     <q-checkbox v-model="selection" val="No flag down of meter" label="No flag down of meter" color="warning"/>
    <br/>
    <q-checkbox v-model="selection" val="Out of line" label="Out of line" color="warning"/>
    </q-list>
    </div>
    <q-item v-model="newReport.date_created"/>
<div class="submit-btn">
    <q-btn class="submit" color="warning" @click="addReport">Submit
    </q-btn>
    </div>
</div>
  </q-layout>
</template>
<script>
import {
  dom,
  event,
  openURL,
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain,
  QTab,
  QTabs,
  QField,
  QInput,
  QCheckbox,
  QRouteTab,
  Dialog,
  QDatetime
} from 'quasar'
import moment from 'moment'

let config = {
  apiKey: "AIzaSyBVXJqLa98z8EwegtYra8jVHv7yrfadfyI",
    authDomain: "taxi-1fd65.firebaseapp.com",
    databaseURL: "https://taxi-1fd65.firebaseio.com",
    projectId: "taxi-1fd65",
    storageBucket: "taxi-1fd65.appspot.com",
    messagingSenderId: "218888618100"
}
var app = firebase.initializeApp(config);
var db = app.database()
let list = db.ref('TaxiList')
var admobid = {};

export default 
 {
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItem,
    QItemSide,
    QItemMain,
    QTab,
    QTabs,
    QField,
    QInput,
    QCheckbox,
    QRouteTab,
    Dialog,
    QDatetime
  },
   data () {
    return {
      selection: [],
      TaxiReport: 'Taxi Report',
      newReport: {
      details:'',
      violation:'',
      plate_number:'',
      date: moment().format('MMM/D/YYYY'),
      date_created: -(new Date().getTime())
      
      }
    }
  },
  firebase: {
  TaxiList: list
      },
  methods : {
    addReport: function (e) {
      this.newReport.violation = this.selection;
      list.push(this.newReport);
      this.newReport.date = '';
      this.newReport.taxi_name = '';
      this.newReport.plate_number = '';
      this.newReport.details= '';
      this.newReport.date_created= '';
      Dialog.create({
      title: 'Submit',
      message: 'Your report was successfully submitted. Please check on the feed tab your report.'
      })
      this.selection=[]
    },
    reportTab (){
      if(AdMob) AdMob.showInterstitial();
      $router.push('/report')
    },
    feedTab (){
      if(AdMob) AdMob.showInterstitial();
      $router.push('/feed')
    }
}

 }
</script>
<style lang="stylus">
.search-bar {
  margin-top:30px;
  margin-right:20px;
  margin-left:20px;
}
.q-toolbar {
  align:center;
}
.body{
  margin: 110px;
}
.q-toolbar-title {
  margin-left: auto;
  margin-right: auto;
  font-weight:13px;
  text-align: center;
}
.logo {
  height:35px;
  width:35px;
  margin-left:120px;
}
.toolbar {
  position:0;
  bottom:0!important;
  width: 100%;
}
.q-item {
  margin-top:10px!important;
  margin-left:-10px;
}
.q-input {
margin-top :-10px;
margin-left:10px;
}
.q-list-header{
  font-size:20px;
  margin-top:10px;
  margin-left:-20px;
}
.data-feed{
  margin-left:30px;
  margin-right:30px;
  margin-bottom:60px;
}
.data-report{
  margin-left:30px;
  margin-right:40px;
  margin-bottom:60px;
}
.q-item {
  font-size:16px;
  margin-top:-10px;
}
.violation-list {
  margin-top:-10px;
}
.button {
  margin-left:80px;
  margin-bottom:30px;
  padding:2px;
}
.q-item-tile {
  margin-top: 20px!important;
}
.q-checkbox {
  padding:5px;
  margin-left:10px;
}
.q-list {
  padding-top:-10px;
  margin-top:20px;
}
.submit-btn {
  margin-left: 120px;
  margin-right: 138px;
  margin-top:-20px;
}
.textarea {
  margin-top:2px;
}
</style>
