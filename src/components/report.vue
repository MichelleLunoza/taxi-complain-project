<template>
  <q-layout>
  <div slot="header">
  <q-toolbar color="primary">
  <q-toolbar-title>{{Complain}}</q-toolbar-title>
  </q-toolbar>

  <q-tabs>
  <q-route-tab
    icon="assignment"
    to="/"
    exact
    slot="title"
    label="feed"    
  />
    <q-route-tab
    icon="report problem"
    to="/report"
    exact
    slot="title"  
    label="report"     
  />
  </q-tabs>
  </div>
<!-- Report Tab -->
<div class="data-report">
    <div>
    <q-item label>Plate Number:</q-item>
    <q-input v-model="newReport.plate_number"/>
    <q-item label>Date:</q-item>
    <q-datetime v-model="newReport.date" type="date" />
    <q-item label>Taxi's Name:</q-item>
    <q-input v-model="newReport.taxi_name" placeholder="ex. GRAB Taxi"/>
    <q-item label>Details:</q-item>
    <q-input class="textarea"
    v-model="newReport.details"
    type="textarea"
    />
    
    <q-list>
    <q-item class="violation-list"label>Violations:</q-item>
     <q-checkbox v-model="selection" val="Refused boarding" label="Refused boarding" />
    <br/>
     <q-checkbox v-model="selection" val="Choosing passengers" label="Choosing passengers" />
    <br/>
     <q-checkbox v-model="selection" val="Over charging" label="Over charging" />
    <br/>
     <q-checkbox v-model="selection" val="No meter" label="No meter" />
    <br/>
     <q-checkbox v-model="selection" val="Tampered or broken meter" label="Tampered or broken meter" />
    <br/>
     <q-checkbox v-model="selection" val="Contracting" label="Contracting" />
    <br/>
     <q-checkbox v-model="selection" val="No receipt" label="No receipt" />
    <br/>
     <q-checkbox v-model="selection" val="Reckless driving" label="Reckless driving" />
    <br/>
     <q-checkbox v-model="selection" val="Rude behavior" label="Rude behavior" />
    <br/>
     <q-checkbox v-model="selection" val="Smoking while driving" label="Smoking while driving" />
    <br/>
     <q-checkbox v-model="selection" val="Not in uniform" label="Not in uniform" />
    <br/>
     <q-checkbox v-model="selection" val="No seatbelts" label="No seatbelts" />
    <br/>
     <q-checkbox v-model="selection" val="Smelly interiors" label="Smelly interiors" />
    <br/>
     <q-checkbox v-model="selection" val="Dirty seats and interiors" label="Dirty seats and interiors" />
    <br/>
     <q-checkbox v-model="selection" val="Left behind items" label="Left behind items" />
    <br/>
     <q-checkbox v-model="selection" val="Physical assault" label="Physical assault" />
    <br/>
     <q-checkbox v-model="selection" val="Verbal harrassment" label="Verbal harrassment" />
    <br/>
     <q-checkbox v-model="selection" val="Malicious mischief" label="Malicious mischief" />
    <br/>
     <q-checkbox v-model="selection" val="Sexual assault" label="Sexual assault" />
    <br/>
     <q-checkbox v-model="selection" val="Dilapidated" label="Dilapidated" />
    <br/>
     <q-checkbox v-model="selection" val="No taxi details inside" label="No taxi details inside" />
    <br/>
     <q-checkbox v-model="selection" val="LPG smells" label="LPG smells" />
    <br/>
     <q-checkbox v-model="selection" val="Texting while driving" label="Texting while driving" />
    <br/>
     <q-checkbox v-model="selection" val="Not giving exact change" label="Not giving exact change" />
    <br/>
     <q-checkbox v-model="selection" val="No flag down of meter" label="No flag down of meter" />
    <br/>
    <q-checkbox v-model="selection" val="Out of line" label="Out of line" />
    </q-list>
    </div>

<div class="submit-btn">
    <q-btn class="submit" color="primary" @click="addReport">Submit
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
      Complain: 'Complain',
      newReport: {
      details:'',
      violation:'',
      plate_number:'',
      name: '',
      date: moment().format('MMM-D-YYYY'),
      }
    }
  },
  firebase: {
  TaxiList: list
      },
  methods : {
    addReport: function () {
      this.newReport.violation = this.selection;
      list.push(this.newReport);
      this.newReport.date = '';
      this.newReport.taxi_name = '';
      this.newReport.plate_number = '';
      this.newReport.details= '';

      Dialog.create({
      title: 'Submit',
      message: 'Your report was successfully submitted. Please check on the feed tab your report.'
      })
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
.q-datetime {
  margin-left:-20px!important;
}
.q-list {
  padding-top:-10px;
  margin-top:20px;
}
.submit-btn {
  margin-top: 30px;
  margin-left: 120px;
   margin-right: 138px;
}
.textarea {
  margin-top:2px;
}
</style>
