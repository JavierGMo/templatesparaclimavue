<template>
    <div v-if="show" class="container-result-place">
        <div class="d-fx f-between">
            <div class="c-form-search">
                <input type="text" v-model="searchLocation" class="ipt-search-place" >
                <button class="btn-search-place" @click.prevent="searchWeatherBTN">search</button>
            </div>
            <div><button class="btn-close" @click="closeSearch"><i class="fas fa-times"></i></button></div>
        </div>
        <div class="place-result"><p>london</p> <i></i></div>
        <div class="place-result"><p>barcelona</p> <i></i></div>
        <div class="place-result"><p>long beach</p> <i></i></div>
    </div>
</template>

<script>
const axios = require('axios');
export default {
    name : 'BaseSearchPlace',
    data(){
        return {
            closeSearchBar : true,
            searchLocation : ''
        }
    },
    props : {
        show : {
            type : Boolean
        }
    },
    methods : {
        closeSearch : function(){
            this.closeSearchBar = !this.show;
            this.$emit('update:barsearch', this.closeSearchBar);

        },
        searchWeatherBTN : async function(){
            console.log('Hola quieres buscar un lugar');
            
            const este = this;
            if(this.searchLocation){
                this.searchLocation = '';
                let url = new URL('http://127.0.0.1:9000/weatherplace');
                const param = this.searchLocation;
                url.search = new URLSearchParams(param);

                try {
                    const res = await fetch(url, {
                        method : 'GET',
                        headers : {
                            'Content-Type': 'application/json'
                        },
                        // body : JSON.stringify({
                        //     location : este.searchLocation
                        // })
                    });
                    const data = await res.json();
                    const weatherDays = data['data'];
                    console.log(weatherDays);
                    este.$emit('update:alldays', weatherDays);
                    
                    
                } catch (err) {
                    console.error(err);
                }
            }
            
            

        }
    }
}
</script>