<template>
    <div class="c-card-w d-fx f-column f-center ">
        <div>
            <p>
                <span v-if="index === 0" class="color-white-light">Tomorrow</span>
                <span v-else class="color-white-light">{{ date }}</span>
            </p>
        </div>
        <div class="d-fx f-center"><img :src="src(day.img_abbr)" alt="icon" class="c-card-img-weat"></div><!--Img card-->
        <div><p><span class="c-temper-max color-white-light">{{ day.max_temp }}°{{ degreesLabel }}</span> <span class="c-temper-min">{{ day.min_temp }}°{{ degreesLabel }}</span></p></div><!--Text-->
    </div><!--Card weather-->
</template>

<script>
export default {
    name : 'BaseCard',
    props : {
        index : {
            type : Number
        },
        day : {
            type : Object,
            default : ()=>({
                'img_abbr' : 'hr',
                'the_temp' : 0,
                'min_temp' : 0,
                'max_temp' : 0,
                'date' : 'Sun, 1 Jan'
            })
        },
        date : {
            type : String,
            default : 'Sum, 1 Jan'
        },
        degreesLabel : {
            type : String,
            default : 'C'
        }
    },
    methods : {
        src : function(routeImage){
            return `https://www.metaweather.com/static/img/weather/${routeImage}.svg`
        },
    }
}
</script>