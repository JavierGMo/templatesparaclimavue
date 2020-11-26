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
            searchLocation : '',
            defaultdegrees : true
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
            // console.log('Hola quieres buscar un lugar');
            
            const este = this;
            if(this.searchLocation){
                
                // let url = new URL();
                const param = this.searchLocation;
                // url.search = new URLSearchParams(param);
                let data = undefined;
                let weatherDays = undefined;
                let signalokres = true;
                
                this.searchLocation = '';

                try {
                    const res = await fetch(`http://127.0.0.1:9000/weatherplace?location=${param}`, {
                        method : 'GET',
                        headers : {
                            'Content-Type': 'application/json'
                        },
                    });
                    if(res.status === 200){

                        data = await res.json();
                        weatherDays = data['data'];
                        this.closeSearchBar = false;
                        //Modificar el nombre del update para cuando la consulta sea correcta
                        this.defaultdegrees = false;
                        this.$emit('update:changedegreesok', this.defaultdegrees);//Cuando es status 200, enviamos un valor para restablecer los valores por defecto en celcius
                        this.defaultdegrees = true;
                    }else if(res.status === 404){
                        alert('Escriba bien el nombre del lugar :)');
                    }else if(res.status === 500){
                        alert('Vaya, tenemos algunos problemas :(');
                    }
                    
                    // console.log(weatherDays);
                    este.$emit('update:alldays', weatherDays);
                    
                    
                } catch (err) {
                    console.error(err);
                }
            }
            
            

        }
    }
}
</script>