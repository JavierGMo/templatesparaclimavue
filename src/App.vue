<template>
  <div id="app" class="d-fx container-principal">
    <BaseAside :datetoday="dateweather().format('ddd, D MMM')" @update:nextdaysweather="nextandtoday($event)" />
    <BaseContent :datanextdays="datanextdays" :todayhightlights="todayhightlights" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import BaseAside from "./components/aside/BaseAside";
import BaseContent from "./components/content/BaseContent";
import moment from 'moment';

export default {
  name: 'App',
  data(){
    return {
      datanextdays : undefined,
      todayhightlights : undefined,
      dateweather : moment,
    }
  },
  components: {
    // HelloWorld,
    BaseAside,
    BaseContent,
  },
  methods : {
    nextandtoday : function(data){
      if(data){
        this.datanextdays = data.nextdays;
        this.todayhightlights = data.hightlights;
        for (let i = 1; i < 6; i++)  this.datanextdays[i].date = this.calculateDate(i);


        console.log(this.datanextdays);
      }
    },
    calculateDate : function(adddays){
            return this.dateweather().add(adddays+1, 'days').format('ddd, D MMM')
    }
  },
}
</script>
