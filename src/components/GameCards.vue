<template>
    <div class="game-area">
        <p>{{answer}}</p>
        <h1 class="title">Poğaça <span>Nerede</span> <strong>?</strong></h1>
        <h4 class="description">Açık kartlardan birini seçtikten sonra, kapalı olan karta tıklayınız</h4>
        <div class="container">
            <transition-group name="rotate-all" appear class="card-container">
                    <app-card
                v-for="(card,index) in cards" 
                :key="index" 
                :card="card"
                @click.native="selectedCard = card.id"
                :class="{'shadow' : selectedCard == card.id}"
                ></app-card>
            </transition-group>
            
        </div>
        <div class="container">
            <transition name="rotate" mode="out-in">
                <component
                @click.native="showCard(answer)"
                :card="answer"
                :is="activeCard">

                </component>
            </transition>
        </div>
    </div>
</template>
<script>
import Card from './Card'
import Defaultcard from './Defaultcard.vue'

export default {
    
    components:{
        appCard :Card,
        appDefaultCard : Defaultcard

    },
    data()
    {
        return{
            selectedCard : null,
            answer : {},
            activeCard  : "app-default-card",
            cards: [
                {id :1 , component : "app-card", image : require('../assets/card-1.jpg') },
                {id :2 , component : "app-card", image : require('../assets/card-2.jpg') },
                {id :3 , component : "app-card", image : require('../assets/card-3.jpg') },
                {id :4 , component : "app-card", image : require('../assets/card-4.jpg') },
                {id :5 , component : "app-card", image : require('../assets/card-5.jpg') },
            ]
        }
    },
    created(){
        let answer = Math.ceil(Math.random()*this.cards.length);
        this.answer = this.cards[answer - 1];
    },
    methods:{
        showCard(answer){
            if(this.selectedCard==null){
                alert("İlk olarak bir kart seçiniz");
            }else{
                this.activeCard = answer.component;
                setTimeout(()=>{  
                    if(answer.id == this.selectedCard){
                        this.$emit("activeComponentEvent","app-celebrate");
                    }else{
                        this.$emit("activeComponentEvent","app-failure")
                }},2000)
              
            }
        }
    }
}
</script>
<style scoped>
.title{
    text-align: center;
    color:rosybrown;
}
.title span{
    color:mediumpurple;
}
.title strong{
    color:darkred;
}
.description{
    color:gray;
    text-align: center;
}
.container, .card-container{
    display:flex;
    justify-content: center;
    align-content: center;
    margin-top:50px;
}
.shadow{
    box-shadow : 0px 5px 48px #055de0!important;
    transition : box-shadow .5s;
}

/*Transition*/

.rotate-all-enter{}
.rotate-all-enter-active{
    animation:rotate-all ease-in-out 1s forwards;
}
.rotate-all-leave{}
.rotate-all-leave-active{}


@keyframes rotate-all {
    from{
transform: rotateY(0);
    }to{
transform: rotateY(1080deg);
    }
}


/*rotate */
.rotate-enter-active{
    animation : rotate-in 1s ease-in-out forwards;    
}
.rotate-leave-active{
    animation : rotate-out 1s ease-in-out forwards;
}

@keyframes rotate-in{
    from{
        transform: rotateY(90deg);
    }to{
        transform: rotateY(0deg);
    }
}

@keyframes rotate-out {
    from{
        transform : rotateY(0deg);
    }to{
        transform: rotateY(90deg);
    }
    
}
</style>  