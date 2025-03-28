
<script>
import Modal from './components/Modal.vue';
import Timer from './components/Timer.vue';

export default {
  data() {
    return {
      modalVisibility:false,
      cursorX: 0,
      cursorY: 0,
      // dots:[0,1,2,3,4,5,6,7,8]
      dots:[0,1] ,
      updateChild_id:null,
      collision_id:null,
      increaseDots_id:null
      // score:0
    };
  },
  components:{
    Modal,
    Timer
  },
  methods: {
    updateMainCursor(event) {
      this.cursorX = event.clientX;
      this.cursorY = event.clientY;
      // updateChildCursor()
      // this.checkCollisions()
      // this.modalCouter=1
    },

    updateChildCursor(){     
      this.dots.forEach((ele,index)=>{
        const dotId = document.getElementById(`dot${index}`); 
        const randomX=Math.random()
      const randomY=Math.random()
      // const randomNumberX = Math.floor(randomX * (window.innerWidth+200)) + 1;
      // const randomNumberY = Math.floor(randomY * window.innerHeight+130) + 1;
      const randomNumberX = Math.floor(randomX * (window.innerWidth + 400)) - 200; 
      const randomNumberY = Math.floor(randomY * (window.innerHeight + 300)) - 150; 

      dotId.style.left=randomNumberX+"px"
      dotId.style.top=randomNumberY+"px"
// console.log("ok the func is running -- --",index)

      })
    },
    checkCollisions(){
      const mainCursor=document.getElementById('main-cursor').getBoundingClientRect()
      // console.log("the details of",mainCursor)
      this.dots.forEach((item,index)=>{
        const childCursor=document.getElementById(`dot${index}`).getBoundingClientRect()   
if(Math.abs(this.cursorX-childCursor.left)<20 && Math.abs(this.cursorY-childCursor.top)<20){
  // throw new Error("it is the collision")
this.modalVisibility=true
console.log("child--",childCursor.left)
console.log("main--",this.cursorX)
// clearInterval(this.updateChild_id); 
// clearInterval(this.collision_id); 
clearInterval(this.increaseDots_id); 
if (!localStorage.getItem('score') || JSON.parse(localStorage.getItem('score')) < this.dots.length) {
  localStorage.setItem('score', JSON.stringify(this.dots.length));
}
}
  })     
    },
    handleResetClicked(){
      this.dots=[0]
      this.modalVisibility=false
      this.increaseDots_id=setInterval(()=>this.dots.length<40 && this.dots.push(this.dots.length),2000)

    }


  },
  mounted() {
    this.updateChild_id= setInterval(this.updateChildCursor, 1500); 
//     setTimeout(() => {
// clearInterval(this.updateChildCursor)
//     },3000)
    // setInterval(this.checkCollisions, 20);
    setTimeout(() => {
  this.collision_id=setInterval(this.checkCollisions, 20); 
}, 2000); 
    this.increaseDots_id=setInterval(()=>this.dots.length<40 && this.dots.push(this.dots.length),1500)
  }
};
</script>


<template>
  <div @mousemove="updateMainCursor" class="w-full h-screen overflow-hidden  relative  main">
    <div id="main-cursor" class="custom-cursor" :style="{ left: cursorX + 'px', top: cursorY + 'px' }">M</div>
   
    <div  v-for="(item,index) in dots" :id="`dot${index}`" :key="item" class="custom-cursor child-cursor" > </div>

    <div style="height: 80px;width: 80px;" class="absolute flex items-center justify-center bottom-10 right-10 text-4xl font-semibold text-white bg-red rounded-full">
{{ dots.length }}
    </div>

    <!-- :style="{ left: cursorX + 'px', top: cursorY + 'px' }" -->
    <!-- <div class="custom-cursor" :style="{ left: cursorX + 'px', top: cursorY + 'px' }">2</div> -->


    <div v-show="modalVisibility" class="w-full h-full absolute top-0 left-0 flex justify-center items-center modal-container">
      <Modal @reset-clicked="handleResetClicked" :user_score="dots.length" />
    </div>

   </div>
</template>



<style>


.custom-cursor {
  position: absolute;
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  background-color: red;
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  /* transition: all 0.1s ease-out; */
}
.child-cursor{
  transition: all 1.5s ease-out;
  background-color: black;
  color: white;
  left: -20px;
  top:100px;
}


.modal-container{
  background: white;
  /* -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px); */
  /* background: rgba(128, 128, 128, 0.519); */
  }
</style>
