<template>
    <div class="c-bar-search">
        <transition name="component-fade" mode="out-in">
            <BaseAsideWeather :datetoday="datetoday" :show="show" :today="today" @update:show="show = $event"/>
        </transition>
        <transition name="component-fade" mode="out-in">
            <BaseSearchPlace :show="show" @update:alldays="sendNextDaysWeather($event)" @update:barsearch="show = $event"/>
        </transition>
    </div>
</template>

<script>
import BaseAsideWeather from "./BaseAsideWeather";
import BaseSearchPlace from "./BaseSearchPlace";
    export default {
        name: 'BaseAside',
        data() {
            return {
                show : false,
                dataNextDays : {},
                today : undefined
            }
        },
        props : {
            datetoday : {
                type : String,
                default : new Date()
            }
        },
        components: {
            BaseAsideWeather,
            BaseSearchPlace,
        },
        methods : {
            sendNextDaysWeather : function(ev){
                const este = this;
                // console.log('Hola');
                // console.log(ev);
                if(ev){
                    // this.allWeather = ev;
                    this.today = ev.dataToday;
                    // this.dataNextDays = ev.dataNextDays;
                    this.$emit('update:nextdaysweather', {
                            hightlights : {
                                windspeed : ev.dataToday.wind_speed,
                                winddirectioncompass : ev.dataToday.wind_direction_compass,
                                humidity : ev.dataToday.humidity,
                                visibility : ev.dataToday.visibility,
                                airpressure : ev.dataToday.air_pressure
                            },
                            nextdays : ev.dataNextDays
                        });
                }
            }   
        }
    }
</script>