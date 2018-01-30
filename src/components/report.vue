<template>
  <q-layout>
  <div slot="header">
  <q-toolbar color="primary">
  <img src="~assets/git.png" class="logo">
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
    <q-input v-model="plate_number"/>
    <q-item label>Taxi Name:</q-item>
    <q-input v-model="taxi_name" />
    <q-item label>Details:</q-item>
    <q-input v-model="details" />
    
    <q-list>
    <q-item class="violation-list"label>Violations:</q-item>
     <q-checkbox v-model="selection" val="option1" label="Refused boarding" />
    <br/>
     <q-checkbox v-model="selection" val="option2" label="Choosing passengers" />
    <br/>
     <q-checkbox v-model="selection" val="option3" label="Over charging" />
    <br/>
     <q-checkbox v-model="selection" val="option4" label="No meter" />
    <br/>
     <q-checkbox v-model="selection" val="option5" label="Tampered or broken meter" />
    <br/>
     <q-checkbox v-model="selection" val="option6" label="Contracting" />
    <br/>
     <q-checkbox v-model="selection" val="option7" label="No receipt" />
    <br/>
     <q-checkbox v-model="selection" val="option8" label="Reckless driving" />
    <br/>
     <q-checkbox v-model="selection" val="option9" label="Rude behavior" />
    <br/>
     <q-checkbox v-model="selection" val="option10" label="Smoking while driving" />
    <br/>
     <q-checkbox v-model="selection" val="option11" label="Not in uniform" />
    <br/>
     <q-checkbox v-model="selection" val="option12" label="No seatbelts" />
    <br/>
     <q-checkbox v-model="selection" val="option13" label="Smelly interiors" />
    <br/>
     <q-checkbox v-model="selection" val="option14" label="Dirty seats and interiors" />
    <br/>
     <q-checkbox v-model="selection" val="option15" label="Left behind items" />
    <br/>
     <q-checkbox v-model="selection" val="option16" label="Physical assault" />
    <br/>
     <q-checkbox v-model="selection" val="option17" label="Verbal harrassment" />
    <br/>
     <q-checkbox v-model="selection" val="option18" label="Malicious mischief" />
    <br/>
     <q-checkbox v-model="selection" val="option19" label="Sexual assault" />
    <br/>
     <q-checkbox v-model="selection" val="option20" label="Dilapidated" />
    <br/>
     <q-checkbox v-model="selection" val="option21" label="No taxi details inside" />
    <br/>
     <q-checkbox v-model="selection" val="option22" label="LPG smells" />
    <br/>
     <q-checkbox v-model="selection" val="option23" label="Texting while driving" />
    <br/>
     <q-checkbox v-model="selection" val="option24" label="Not giving exact change" />
    <br/>
     <q-checkbox v-model="selection" val="option25" label="No flag down of meter" />
    <br/>
    <q-checkbox v-model="selection" val="option26" label="Out of line" />
    </q-list>
    </div>

<div class="submit-btn">
    <q-btn class="submit" color="primary" >Submit</q-btn>
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
  QRouteTab
} from 'quasar'


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
    QRouteTab
  },
   data () {
    return {
      selection: ['option1', 'option2', 'option3', 'option4',
      'option5', 'option6', 'option7', 'option8', 'option9', 
      'option10', 'option11', 'option12', 'option13', 'option14',
      'option15', 'option16', 'option17', 'option18', 'option19',
      'option20', 'option21', 'option22', 'option23', 'option24',
      'option25', 'option26'],
      Complain: 'Complain',
      model: new Date(), // as in "right this moment"
      taxi_name:'',
      details:'',
      violation:'',
      plate_number:'',
    }
  },
  methods : {
    addReport: function () {
      TaxiListRef.push(this.addReport);
      this.addReport.taxi_name = '';
      this.addReport.violation = '';
      this.addReport.plate_number = '';
      this.addReport.details= '';
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
