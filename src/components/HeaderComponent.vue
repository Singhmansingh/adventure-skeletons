<template>
    <div id="header">
        <h1 @click="navigate">Adventure Skeletons!</h1>
        <h2>An RPG by Grant Howitt and Chris Taylor</h2>
    </div>
</template>

<script>
export default {
    name:"HeaderComponent",
    methods:{
        navigate(){
            window.open("https://gshowitt.itch.io/adventure-skeletons","_blank")
        }
    }
}
</script>
<style scoped>
#header {
    flex-shrink:1;
    justify-content: center;
    flex-direction: column;
    align-items: center ;
    display: flex;
    font-family: "Skeleton";
    background: rgb(39, 39, 39);
    font-size: 2em;
    padding: 10px;
    border-top-left-radius: 100px;
    border-top-right-radius: 100px;
}

    h2 {
        font-size: 0.5em;

    }

    h1 {
        margin:20px;
                cursor: pointer;
        user-select: none;
    }
</style>