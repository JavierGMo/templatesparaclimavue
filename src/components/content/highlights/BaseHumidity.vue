<template>
    <div class="c-card-general d-fx f-column f-center">
        <div><p><span>Humidity</span></p></div>
        <div><p class="color-white-light"><span class="txt-today-weather">{{ humidity }}</span><span class="color-gray-fifty txt-complement-weather">%</span></p></div>
        <div class="content-bar-humidity p-relative">
            <div class="p-absolute posi-top-humidity pos-0">0</div>
            <div class="p-absolute posi-top-humidity pos-50">50</div>
            <div class="p-absolute posi-top-humidity pos-100">100</div>
            <div class="p-absolute posi-bottom-humidity pos-percentagee">%</div>
            <progress max="100" :value="humidity"></progress><!--bar humidity-->
        </div>
        
    </div><!--humidity-->
</template>

<script>
export default {
    name : 'BaseHumidity',
    props : {
        humidity : {
            type : Number,
            default : 0
        }
    }
}
</script>