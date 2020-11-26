<template>
    <div v-if="!show">
        <div class="d-fx f-between contain-btns-search">
            <div><button class="c-btn-search-p" @click="openSearch">Search for places</button></div>
            <div><button class="c-btn-rounded"><i class="fas fa-location-arrow"></i></button></div>
        </div>
        <div class="d-fx f-column f-center">
            <div class="d-fx f-center containt-img-bar"><img :src="src(today.img_abbr)" alt="" class="img-bar"></div>
            <!-- <div class="cont-deegree"><p class="color-white-light"><span class="txt-deegree-unit-bar">{{ today.the_temp }}</span><span class="txt-deegree-measure-bar color-gray-fifty">°{{ unitMeasure }}</span></div> -->
            <div class="cont-deegree">
                <p class="color-white-light">
                    <span class="txt-deegree-unit-bar">{{ degreechangebaw?celsius():fahrenheit() }}</span><span class="txt-deegree-measure-bar color-gray-fifty"> °{{degreesLabel}}</span>
                </p>
                <!-- degreechangebaw?celsius():fahrenheit() -->
            </div>
            <div class="weather-state-bar">
                <p><span class="weather-state-bar">{{ today.weather_state_name }}</span></p>
            </div>
        </div>
        <div class="d-fx f-column f-center c-today">
            <div>
                <p class="color-gray-fifty">Today . {{ datetoday }}</p>
            </div>
            <div>
                <p class="color-gray-fifty"><i class="fas fa-map-marker-alt"></i> {{ today.place }}</p>
            </div>
        </div>
    </div>
</template>

<script>
// 'date' : moment.format('D, d M'),
export default {
    name : 'BaseAsideWeather',
    data(){
        return {
            auxShow : false,
            degreesLabel : 'C',
            auxdegreechangebaw: true,
            auxdefaultdegree : true,
        }
    },
    props : {
        show : {
            type : Boolean
        },
        today : {
            type: Object,
            default : ()=>({
                'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'place' : 'loading...',
                'weather_state_name' : 'loading...',
                'wind_speed' : 0,
                'wind_direction_compass' : 'loading...',
                'humidity' : 0,
                'visibility' : 0,
                'air_pressure' : 0
            })
        },
        datetoday : {
            type : String,
            default : new Date()
        },
        degreechangebaw : {
            type : Boolean,
            default : true
        },
        statedegree : {
            type : Boolean,
            default : true
        }
    },
    methods : {
        openSearch : function(){
            this.auxShow = !this.auxShowshow;

            this.$emit('update:show', this.auxShow);
        },
        src : function(routeImage){
            return `https://www.metaweather.com/static/img/weather/${routeImage}.svg`
        },
        celsius : function(){
            this.degreesLabel = 'C';
            return this.today['the_temp'];
            // return this.today['the_temp']?Math.round(((this.today['the_temp']-32)*(5/9))):0;
        },
        fahrenheit : function(){
            this.auxdefaultdegree = !this.statedegree;
            this.degreesLabel = 'F';
            return Math.round((this.today['the_temp']*(9/5)))+32;
        },
        degreeAction : function(flagchange){
            //Esta funcion se puede usar para cambiar el label, solo es una opcion
            return flagchange?'C':'F';
        },
        determineDegree : function(){
            let label = 'c';
            
            if(this.degreechangebaw){
                label = 'C';
            }else{
                label = 'f';
                if(!this.statedegree){
                    label = 'ce';
                }else{
                    label = 'fa';
                }
            }
            
            return label;
        }
    }
}
</script>