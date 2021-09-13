<template>
    <div class="container">
        <h1>Tebrikler Bildiniz!</h1>
        <button @click="newGame">Yeni Oyun</button>
        <br>

        <button @click="start">Start</button>
    </div>
</template>
<script>
 import Vue from 'vue'
  import VueConfetti from 'vue-confetti'
  Vue.use(VueConfetti)
export default {
    
    methods : {
        newGame(){
            this.$emit("activeComponentEvent","app-game-cards");
            this.$confetti.stop();
        }
    },
    created() {
        this.$confetti.start();
    }
    
}
</script>
<style scoped>
.container{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    top:0;
    bottom:0;
    right: 0;
}
.container h1{
    text-align: center;
    font-size: 333%;
    color:darkgreen;
    opacity: .5;
}
.container button{
    cursor:pointer;
    width: 200px;
    background-color: #ffff;
    color:darkred;
    border:1px solid darkgreen;
    height: 50px;
    font-size:15px;
    border-radius: 5px;
    outline: none;
    transition:all 1s;
}
.container button:hover{
    background-color: darkgreen;
    color:#ffff;
    transition:all 1s;
}
</style>