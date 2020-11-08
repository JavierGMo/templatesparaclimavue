<template>
  <div id="app" class="d-fx container-principal">
    <BaseAside 
        @update:updatedataweather="signalforchangestate($event)"
        @update:nextdaysweather="nextandtoday($event)"
        :datetoday="dateweather().format('ddd, D MMM')"
        :degreeChange="degreeChange"
        :statedegree="statedegree" />
    <BaseContent
        @update:degreessignal="degreeschange($event)"
        :datanextdays="datanextdays"
        :todayhightlights="todayhightlights"
        :dates="datesw"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import BaseAside from "./components/aside/BaseAside";
import BaseContent from "./components/content/BaseContent";
import moment from 'moment';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    BaseAside,
    BaseContent,
  },
  data(){
    return {
      datanextdays : undefined,
      todayhightlights : undefined,
      dateweather : moment,
      datesw : undefined,
      degreeChange : undefined,
      statedegree : true
    }
  },
  methods : {
    nextandtoday : function(data){
      if(data){
        this.datesw = [];
        this.datanextdays = data.nextdays;
        this.todayhightlights = data.hightlights;
        // for (let i = 1; i < 6; i++)  this.datanextdays[i].date = this.calculateDate(i);
        for (let i = 1; i < 6; i++)  this.datesw.push(this.calculateDate(i));

        // console.log(this.datanextdays);
      }
    },
    calculateDate : function(adddays){
      return this.dateweather().add(adddays, 'days').format('ddd, D MMM')
    },
    degreeschange : function(degree){
        this.degreeChange = !degree;
    },
    signalforchangestate : function (signal) {
        this.statedegree = signal;
        console.log('sognak: ' + signal);
    }
  }
}
</script>
