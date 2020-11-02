<template>
    <div>
        <div>Hola</div>
        <p>{{value}}</p>
    </div>
</template>

<script>
    export default {
        name : 'BaseAuxCont',
        props : {
            value : {
                type : String,
                default : ''
            }
        }
    }
</script>