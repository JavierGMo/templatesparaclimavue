<template>
    <div class="c-card-general d-fx f-column f-center">
        <div><p><span><!--Visibility-->{{title}}</span></p></div>
        <div><p class="color-white-light"><span class="txt-today-weather">{{ highlight }}</span><span class="color-gray-fifty txt-complement-weather">{{messaure}}</span></p></div>
    </div>
</template>

<script>
export default {
    name : 'BaseGeneralHighlight',
    props : {
        title : {
            type : String,
            default : 'loading...'
        },
        highlight : {
            type : Number,
            default : 0
        },
        messaure : {
            type : String,
            default : 'loading...'
        }
    }
}
</script>