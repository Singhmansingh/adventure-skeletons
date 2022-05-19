<template>
    <div id="footer">
        <h3>The Human "Dungeon"</h3>
        <div id="selector-container">
        <select id="adventureSelector">
            <option v-for="(setting, index) in settings" :key="'setting-'+index" :value="setting">{{setting}}</option>
        </select>
        </div>

    </div>
</template>

<script>
import * as DATA from './data.json'
export default {
    name:"FooterComponent",
    setup(){
        const settings = DATA.humanDungeon;
        return {
            settings
        }
    }
}
</script>

<style scoped>
#footer {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    padding-left: 20%;
    padding-right: 20%;
}
    #selector-container {
        flex:1;
    }
    h3 {
        flex:1;
        font-size: 2em;
        margin:10px;
    }
</style>