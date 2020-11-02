<template>
    <div class="c-content-weather">
        <div class="c-content-units d-fx f-fend">
            <!-- <div><button class="c-btn-rounded c-btn-deegree" @click="showDeegrees = !showDeegrees" v-bind:class="[showDeegrees ? cDeegreeSelect : '']">°{{ unitMeasure }}</button></div>
            <div><button class="c-btn-rounded c-btn-deegree" @click="showDeegrees = !showDeegrees" v-bind:class="[!showDeegrees ? cDeegreeSelect : '']">°F</button></div> -->
            <!-- <div><button class="c-btn-rounded c-btn-deegree" v-on:click="celsius" v-bind:class="[showDeegrees ? cDeegreeSelect : '']">°C</button></div>
            <div><button class="c-btn-rounded c-btn-deegree" v-on:click="fahrenheit" v-bind:class="[!showDeegrees ? cDeegreeSelect : '']">°F</button></div> -->
        </div>
        <div class="c-contents-cards d-fx f-center">
            <BaseCard
                v-for="(day, index) in datanextdays"
                :key="index"
                :day="day"
                :index="index" />
        </div><!--cards-->
        <div>
            <div><h4>Today's Hightlights</h4></div>
            <div class="d-fx contain-cards-weather f-center">
                <div class="d-fx card-info-today">
                    <BaseWind  :windspeed="todayhightlights.windspeed" :winddirectioncompass="todayhightlights.winddirectioncompass" />
                    <BaseHumidity :humidity="todayhightlights.humidity" />
                </div><!--wind status and humidity-->
                <div class="d-fx card-info-today">
                    <BaseGeneralHighlight :title="'Visibility'" :highlight="todayhightlights.visibility" :messaure="'miles'" /><!--visibility-->
                    <BaseGeneralHighlight :title="'Air pressure'" :highlight="todayhightlights.airpressure" :messaure="'mb'" /><!--Air pressure-->
                    <!--Pasa el nombre y la unidad de medida-->
                </div><!--visibility and air pressure-->
            </div><!--Data Hightlights-->
        </div><!--Hightlights-->
        <div>
            <div><p>Javier Mora &copy; DevChallenges</p></div>
        </div><!--footer-->
    </div><!--Content data weather-->
</template>



<script>
import BaseCard from "./BaseCard";
import BaseWind from "./highlights/BaseWind";
import BaseHumidity from "./highlights/BaseHumidity";
import BaseGeneralHighlight from "./highlights/BaseGeneralHighlight";

//fecha().format('ddd, D MMM')
export default {
    name : 'BaseContent',
    components : {
        BaseCard,
        BaseWind,
        BaseHumidity,
        BaseGeneralHighlight,
    },
    props : {
        datanextdays : {
            type : Array,
            default : ()=>([
                {'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'},
                {'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'},
                {'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'},
                {'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'},
                {'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'}
            ])
        },
        todayhightlights : {
            type : Object,
            default : ()=>({
                windspeed : 0,
                winddirectioncompass : 'loading',
                humidity : 0,
                visibility : 0,
                airpressure : 0,
            })
        },
    },
    methods : {
        
    }
}
</script>