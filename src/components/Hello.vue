<template>
  <q-layout>
  <div slot="header">
  <q-toolbar color="secondary">
  <q-toolbar-title>{{Complain}}</q-toolbar-title>
  </q-toolbar>

  <q-tabs v-model="selectedTab" color="secondary">
  <q-route-tab
    icon="assignment"
    to="/"
    exact
    slot="title"
    label="feed"  
    name="tab-1"
    align="center"  
  />
    <q-route-tab
    icon="report problem"
    to="/report"
    exact
    slot="title"  
    label="report"  
    name="tab-2"   
    align="center"
  />
  </q-tabs>
  </div>


<q-btn
  @click="$router.push('/report')"
  round
  color="secondary"
  class="fixed-bottom-right animate-pop"
  style="margin: 0 15px 15px 0" 
>
  <q-icon name="add" />
</q-btn>
      <!--
        Use <q-side-link> component
        instead of <q-item> for
        internal vue-router navigation
      -->
<div class="search-bar">
<q-search v-model="search" placeholder="Search Taxi Plate Number"></q-search>
</div>
</div>
<div class="data-feed">
    <q-list-header>Reports</q-list-header>
      <q-list v-for='taxi in TaxiList.slice(0, 5)' :key="taxi.date_created">
      <p> <strong> Created Report: </strong>{{taxi.date_created | formattedDate }} </p>
      <p> <strong> Date of Incident: </strong> {{taxi.date}} </p>
      <p> <strong> Plate Number: </strong> {{taxi.plate_number}} </p>
      <p> <strong> Taxi's Name: </strong> {{taxi.taxi_name}} </p>
      <p>  <strong> Violations: </strong>   </p>
      <q-item v-for='item in taxi.violation' :key="taxi.id"><li class="bullet">{{item}}</li></q-item>
      <p> <strong> Details: </strong> {{taxi.details}}</p>
    </q-list>
</div>
<q-pagination v-model="page" :min="minPages" :max="maxPages" />
<!--
<div class="button">
<q-btn icon="keyboard arrow left" disabled>New</q-btn><q-btn icon="keyboard arrow right">Older</q-btn>
</div>-->
  </q-layout>
</template>

<script>

import moment from 'moment'
Vue.filter('formattedDate',function(value){
  var rawdate = value.toString().replace('-','');
  return moment(new Date(parseInt(rawdate))).format('MMM/D/YYYY hh:mm: A')
});

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
  QSearch,
  QRouteTab,
  QPagination
} from 'quasar'

import Vue from 'vue'

var VueFire = require('vuefire')
var firebase = require('firebase')
Vue.use(VueFire)

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
let list = db.ref('TaxiList').orderByChild('date_created')

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
    QSearch,
    QRouteTab,
    QPagination
  },
   data () {
    return {
      selectedTab: 'tab-1',
      Complain: 'Taxi Complain',
      search: '',
      plate_number:[],
      page: 1,
      minPages: 1,
      maxPages: 10
    }
  },
    firebase: {
    TaxiList: list
  },
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
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  font-weight:13px;
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
  margin-bottom:-20px!important;
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
  margin-top: 30px;
  margin-left: 120px;
   margin-right: 138px;
}
.bullet {
  margin-left:15px;
  margin-top:-30px;
  list-style-type: circle;
}
p {
margin-left:10px;
}
.q-pagination {
  margin-left:90px;
  margin-right:50px;
  margin-bottom:40px;
}
</style>
