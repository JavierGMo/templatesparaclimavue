<template>
    <div class="c-card-general d-fx f-column f-center">
        <div><p><span>Wind status</span></p></div>
        <div><p class="color-white-light"><span class="txt-today-weather">{{ windspeed }}</span><span class="color-gray-fifty txt-complement-weather">mph</span></p></div>
        <div class="content-wind-status"><p><i class="far fa-compass"></i> <span>{{ winddirectioncompass }}</span></p></div>
    </div><!--wind status-->
</template>

<script>
    export default {
        name : 'BaseWind',
        props : {
            windspeed : {
                type : Number,
                default : 0
            },
            winddirectioncompass : {
                type : String,
                default : 'loading...'
            }
        }
    }
</script>