<template>
    <div class="c-bar-search">
        <transition name="component-fade" mode="out-in">
            <BaseAsideWeather
                @update:show="show = $event"
                :datetoday="datetoday"
                :show="show"
                :today="today"
                :degreechangebaw="degreeChange"
                :statedegree="defaultflagdegree" />
        </transition>
        <transition name="component-fade" mode="out-in">
            <BaseSearchPlace
                @update:alldays="sendNextDaysWeather($event)"
                @update:barsearch="barsearchchange($event)"
                @update:changedegreesok="funcdefaultdegrees($event)"
                :show="show" />
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
                today : undefined,
                defaultflagdegree : true,
            }
        },
        props : {
            datetoday : {
                type : String,
                default : new Date()
            },
            degreeChange : {
                type : Boolean,
                default : true
            },
            statedegree : {
                type : Boolean,
                default : true
            }
        },
        components: {
            BaseAsideWeather,
            BaseSearchPlace,
        },
        methods : {
            sendNextDaysWeather : function(ev){
                const este = this;
                if(ev){
                    this.today = ev.dataToday;
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
            },
            barsearchchange : function(change){
                this.show = change;
                this.$emit('update:updatedataweather', this.show);
            },
            funcdefaultdegrees : function(param){//fun para restablecer los valores por defecto en los grados y en el label de grados
                this.defaultflagdegree = param;
                this.$emit('update:cardsupdatedegree', this.defaultflagdegree);
            }
        }
    }
</script>