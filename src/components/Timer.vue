
<script>  

export default{
    name:'Timer',
    data(){
        return{
            timerValue:0
        }
    },
    mounted(){
        // setInterval(()=>,1000)
    }
}


</script>

<template>
    <div class="absolute bottom-10 right-10 text-3xl font-semibold text-white bg-red">
{{ timerValue }}
    </div>

</template>