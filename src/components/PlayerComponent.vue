<template>
    <div id="player">
        <div id="skeleton">
            <div class="part head" :style="{opacity: health.head/maxHealth.head}" @contextmenu="e=> increaseMaxHealth('head',e)" @click="reduceHealth('head')"><div class="skele-overlay">{{maxHealth.head}}</div></div>
            
            <div class="middle">
                <div class="part left-arm" :style="{opacity: health.leftArm/maxHealth.leftArm}" @contextmenu="e=> increaseMaxHealth('leftArm',e)" @click="reduceHealth('leftArm')"  ><div class="skele-overlay">{{maxHealth.leftArm}}</div></div>
                <div class="part torso" :style="{opacity: health.torso/maxHealth.torso}" @contextmenu="e=> increaseMaxHealth('torso',e)" @click="reduceHealth('torso')"><div class="skele-overlay">{{maxHealth.torso}}</div></div>
                <div class="part right-arm" :style="{opacity: health.rightArm/maxHealth.rightArm}" @contextmenu="e=> increaseMaxHealth('rightArm',e)" @click="reduceHealth('rightArm')"><div class="skele-overlay">{{maxHealth.rightArm}}</div></div>
            </div>

            <div class="part pelvis" :style="{opacity: health.pelvis/maxHealth.pelvis}" @contextmenu="e=> increaseMaxHealth('pelvis',e)" @click="reduceHealth('pelvis')"><div class="skele-overlay">{{maxHealth.pelvis}}</div></div>

            <div class="bottom">
                <div class="part left-leg" :style="{opacity: health.leftLeg/maxHealth.leftLeg}" @contextmenu="e=> increaseMaxHealth('leftLeg',e)" @click="reduceHealth('leftLeg')"><div class="skele-overlay">{{maxHealth.leftLeg}}</div></div>
                <div class="part right-leg" :style="{opacity: health.rightLeg/maxHealth.rightLeg}" @contextmenu="e=> increaseMaxHealth('rightLeg',e)" @click="reduceHealth('rightLeg')"><div class="skele-overlay">{{maxHealth.rightLeg}}</div></div>
            </div>

        </div>
        <div id="stats">
            <div ref="nameEntry" spellcheck="false" id="name" class="border" @change="change('name')" contenteditable="">Name</div>
            <div ref="dataEntry" id="ancestry" class="border">
                <select id="ancestry-list" @change="changeAncestry($event)">
                    <option disabled value="" selected>Select your Ancestry...</option>
                    <option v-for="(a,index) in ancestries" :key="'ancestry-'+a" :value="index" >{{a.name}}</option>
                </select>
            </div>
            <div  id="bonus" class="border" :style="{opacity: bonus ? 1 : 0.4}">{{bonus ? bonus : "Ancestry Bonus"}}</div>
            <div id="equiptment" class="border">
                <div class="item" v-for="(itemIndex,index) in equiptment" :key="'eq-'+index" :title="equiptmentList[itemIndex].bonus">
                    <img class="item-image" :src="'/imgs/items/'+equiptmentList[itemIndex].img"  @click="changeEquiptment(index)">
                </div>
            </div>

        </div>
    </div>
    <div class="modal" v-if="modalVisible">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Select your Equiptment</div>
                <div class="modal-close" @click="modalVisible = false">X</div>
            </div>
            <div class="modal-body">
                    <div class="modal-list">
                        <div class="item" v-for="(item,index) in equiptmentList" :key="'equiptment-'+index" @click="setEquiptment(index)" :title="item.bonus">
                            <img class="item-image" :src="'/imgs/items/'+item.img"/>
                            <p>{{index +1}}. {{item.name}}</p>
                        </div>
                    </div>
                   
            </div>
        </div>
    </div>
</template>

<script>
import * as DATA from './data.json';
export default {
    name:"PlayerComponent",
    setup(){
        const ancestries = DATA.ancestry;
        const equiptmentList = DATA.equiptment;
        const treasures = DATA.treasure;
        return{
            ancestries,
            equiptmentList,
            treasures,
        }
    },
    created(){
        window.addEventListener('keydown', (e) => {
            if(e.key == "Control") this.pressingCtrl = true;
        })
        window.addEventListener('keyup', (e) => {
            if(e.key == "Control") this.pressingCtrl = false;
        })
    },
    data(){
        return {
            name: "",
            pressingCtrl:false,
            ancestry: "",
            bonus:"",
            modalVisible: false,
            equiptment: [0,0],
            activeIndex:0,
            maxHealth:{
                head: 2,
                leftArm: 2,
                rightArm: 2,
                torso: 2,
                 leftLeg: 2,
                 rightLeg: 2,
                 pelvis: 2
            },
            health:{
                head: 2,
                leftArm: 2,
                rightArm: 2,
                torso: 2,
                 leftLeg: 2,
                 rightLeg: 2,
                 pelvis: 2
            }
        }
    },
    methods:{
        changeName(e){
            this.name = e.target.textContent
        },
        changeAncestry(e){
            let index = e.target.value;
            this.ancestry = this.ancestries[index].name;
            this.bonus = this.ancestries[index].bonus;

            if(this.ancestry == "Dwarf"){
                 this.maxHealth.head = 3;
                 this.health.head = 3;
                    this.maxHealth.torso = 3;
                    this.health.torso = 3;
            }
            else {
                this.maxHealth = {
                head: 2,
                leftArm: 2,
                rightArm: 2,
                torso: 2,
                 leftLeg: 2,
                 rightLeg: 2,
                 pelvis: 2
            }
            }
        },
        changeEquiptment(index){
            this.activeIndex = index;
            this.modalVisible = true;
        },
        setEquiptment(itemIndex){
            this.equiptment[this.activeIndex] = itemIndex;
            this.modalVisible = false;
        },
        reduceHealth(part){
            if(this.health[part] > 0) this.health[part]--; 
            else this.health[part] = this.maxHealth[part]
        },
        increaseMaxHealth(part,e){
            e.preventDefault();
            if(this.pressingCtrl){
                this.maxHealth[part] = 2;
                this.health[part] = 2;
                return;
            }
            this.maxHealth[part]++;
            this.health[part]++;
        }
    },
    mounted(){
        this.$refs.nameEntry.addEventListener('input', (e) => {
            this.changeName(e);
        } )
    }
}
</script>
<style scoped lang="scss">

.border {
    box-sizing: border-box;
    border: 2px solid rgb(65, 65, 65);

}

#player {
    width: 300px;
    height:  600px;
        display: flex;
    align-items: center;
    justify-content: center;
    color: black;
    flex-direction: column;
}

@mixin background-picture($src){
    background-image: url('../assets/imgs/'+ $src);
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
}

.skele-overlay{
    position:absolute;
    width: 30px;
    height: 30px;
    border: 2px solid black;
    background:white;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
    left: 0;
    pointer-events: none;
font-size: 1.4em;
font-weight: bold;

}

.skele-overlay-bottom {
    bottom:0;
}

#skeleton {
    flex:3;
        border-top-left-radius: 90px;
 border-top-right-radius: 90px;
    user-select: none;
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
    background:linear-gradient(#ffffff 10%, #444444 90% );
    display: flex;
    align-items: center;
    flex-direction: column;

    
    .part{
        cursor: pointer;
                position:relative;

    }
    .head {
        flex:3;
        width: 100%;
        @include background-picture("head.png");
               .skele-overlay {
                left: 70px;
            }
    }
    
    

    .middle {
        flex:4;
        display: flex;
        flex-direction: row-reverse;
        width: 100%;
        div {
            flex:1;
        }

        .left-arm,.right-arm {
            margin: 25px 0 25px 0;

        }

        .left-arm {
            @include background-picture("left-arm.png");
            .skele-overlay {
                left:80px;
                bottom:-40px;
            }
        }
        .right-arm {
            @include background-picture("right-arm.png");
            .skele-overlay {
                left: 0;
                bottom:-40px;
            }
        }
        .torso {
            @include background-picture("torso.png");
            margin: 0 -30px 0 -30px;
              .skele-overlay {
                left: 100px;
                top:-20px;
            }
        }
    }

    .pelvis {
         flex:1;
        width: 100%;
        margin: 0 0 -10px 0;
        @include background-picture("pelvis.png");
        .skele-overlay {
                left: 80px;
            }
    }

    .bottom {
        flex:6;
        display: flex;
        flex-direction: row-reverse;
        justify-content: center;
        width: 60%;
        div {
            flex:1;
            
        }
        .left-leg {
            @include background-picture("left-leg.png");
            .skele-overlay {
                bottom:0;
                left: 80px;
            }
        }
        .right-leg {
            @include background-picture("right-leg.png");
            .skele-overlay {
                bottom:0;
                left:-50px;
            }
        }
    }
}

#stats {
    flex:2;
        width: 100%;

        gap: 5px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    color:white;
    background:rgb(24, 24, 24);
     div {
        flex:2;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 5px;
    }
    #name {
        font-family: "Skeleton";
        font-size: 1em;
    }

    #bonus {
        font-size: 1.2em
    }
}

#equiptment {
    flex:3 !important;
    
    img {
        width: 50%;
    }
}






.modal {
    width:100%;
    height: 100%;
        font-size: 1.75em;

    position:absolute;
    background: rgba(0, 0, 0, 0.74);
    top: 0;
    z-index: 20;
    display: flex;
    justify-content: center;
    align-items: center;
    .modal-content{
        width: 60%;
        background:grey;
        display: flex;
        flex-direction: column;
        div {
            padding: 10px;
            box-sizing: border-box;
        }
        .modal-header {
            flex-shrink:1;
            width: 100%;
            background: rgb(41, 41, 41);
            flex-direction: row;
            display: flex;
            align-items: center;
            justify-content: stretch;
            .modal-title {
                flex:1;
            }
            .modal-close {
                cursor:pointer;
                user-select: none;
            }
        }
        .modal-body {
            flex:1;
            width: 100%;
            background: rgb(5, 5, 5);
            display: flex;
            flex-direction: column;



            .modal-list {
                width:100%;
            justify-content: space-evenly;
            flex-wrap: wrap;
            display:flex;
            flex-direction: row;
            width: 100%;
            }
        }
        .modal-footer {
            flex-shrink:1;
            width: 100%;
            background: rgb(0, 255, 98);
        }
    }

}

            .item {
                width: 150px;
                cursor:pointer;
                .item-image {
                    width: 100%;
                }
            }


</style>