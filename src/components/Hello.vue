<template>
  <q-layout>
  <div slot="header">
  <q-toolbar color="primary">
  <img src="~assets/git.png" class="logo">
  <q-toolbar-title>Complain</q-toolbar-title>
  </q-toolbar>

  <q-tabs>
  <q-tab name="xtab-1" label="feed" icon="assignment" slot="title" />
  <q-tab name="xtab-2" label="report" icon="report problem" slot="title" />
  </q-tabs>
  </div>
<q-btn
  v-back-to-top.animate="{offset: 500, duration: 200}"
  round
  color="primary"
  class="fixed-bottom-right animate-pop"
  style="margin: 0 15px 15px 0"
>
  <q-icon name="keyboard_arrow_up" />
</q-btn>
      <!--
        Use <q-side-link> component
        instead of <q-item> for
        internal vue-router navigation
      -->
<div class="search-bar">
<q-search v-model="searchModel"></q-search>
</div>
<div class="data-feed">
    <q-list-header>Data Feed</q-list-header>
      <q-list v-for='taxi in TaxiList':key="taxi.id">
      <q-item label> {{taxi}} </q-item>
    </q-list>
</div>


<div class="button">
<q-btn icon="keyboard arrow left" disabled>New</q-btn><q-btn icon="keyboard arrow right">Older</q-btn>
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
  QSearch
} from 'quasar'

import Vue from 'vue'

var VueFire = require('vuefire')
var firebase = require('firebase')
Vue.use(VueFire)

let config = {
  apiKey: 'AIzaSyBVXJqLa98z8EwegtYra8jVHv7yrfadfyI',
  authDomain: 'taxi-1fd65.firebaseapp.com',
  databaseURL: 'https://taxi-1fd65.firebaseio.com',
  projectId: 'taxi-1fd65',
  storageBucket: 'taxi-1fd65.appspot.com',
  messagingSenderId: '218888618100'
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
    QSearch
  },
   data () {
    return {
      selection: ['option1', 'option2', 'option3', 'option4',
      'option5', 'option6', 'option7', 'option8', 'option9', 
      'option10', 'option11', 'option12', 'option13', 'option14',
      'option15', 'option16', 'option17', 'option18', 'option19',
      'option20', 'option21', 'option22', 'option23', 'option24',
      'option25', 'option26'],
      model: new Date() // as in "right this moment"
    }
  },
    firebase: {
    TaxiList: list
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
.img{
  align:center;
}
.q-toolbar-title {
  text-align:left;
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
  margin-top:10px;
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
</style>
