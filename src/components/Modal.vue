

<script> 
export default{
    name:'Modal',
    props:{
        user_score:String
    },
    data(){
        return{
highest_score:JSON.parse(localStorage.getItem('score')) || null
        }
    },
  
}
</script>

<template>
<div  class="rounded-lg  flex flex-col justify-center gap-10 items-center modal-box">

<div class="flex flex-col items-center ">
    <img src="/game_over.png" width="150px" height="150px" class="object-fit-contain" alt="load..." />

<p  class="text-4xl text-red"> - Contact<span style="font-size: 50px">0 </span>-</p>
</div>
<p  class="text-3xl text-red">GAME OVER</p>

<p  style="color: red;" class="text-2xl"> <span class="text-black ">Score:</span> {{ user_score }} </p>
<p v-show="highest_score" style="color: red;" class="text-2xl"> <span class="text-black ">Highest Score:</span> {{ highest_score }} </p>

<button  @click="$emit('reset-clicked')" type="button" class="mt-10 rounded-lg bg-red text-white border-none font-medium pointer">Try Again</button>



</div>
</template>

<!-- <button  @click="$emit('reset-clicked')" type="button" class="rounded-lg border-none font-medium pointer">reset</button> -->

<style scoped>
.modal-box{
    width: 350px;
    height:max-content; 
     /* border: 1px solid gray; */
     padding: 20px 10px;
     -webkit-box-shadow: 4px 5px 8px 3px rgba(0,0,0,0.75);
-moz-box-shadow: 4px 5px 8px 3px rgba(0,0,0,0.75);
box-shadow: 4px 5px 8px 3px rgba(0,0,0,0.75);

}
button{
padding:10px 40px ;
    font-size:16px;

}

</style>