<template>
    <div class="mappointpage" v-show="closeflag" >
   
      <div class="closepage" @click="clickme() ">×</div>
<div class="content">   <slot></slot></div>

    </div>
</template>

<script>

export default{
  data() {
    return {
     closeflag:false
    };
  },
  methods:{
clickme(){
  // console.log('father',this.fatherFlag);
  // console.log('this.closeflag',this.closeflag);
this.$emit('closecommappointpage');
}
  },
  props:['fatherFlag'],
  watch:{
    'fatherFlag':function(newval){
this.closeflag=newval;
    }
  }
}
</script>

<style>
.mappointpage{
	height:3rem;
	width:4rem;
	position:fixed;
	top:50%;
	left:50%;
	transform:translateX(-50%) translateY(-50%);
	z-index:1000;
  background: rgba(89, 195, 220, 0.6);

box-sizing: border-box;
  }
 .closepage{
   box-sizing: border-box;
    height:0.22rem;
    width:0.3rem;
    top:0;
    right:0 ;
    position: absolute;
  
line-height: 0.2rem;
text-align: center;
font-size: 0.2rem;
color: rgba(255, 0, 0, 0.6);
  }
   .closepage:hover{  
     border: 1px solid rgba(89, 195, 220, 1);
color: rgba(255, 0, 0, 0.9);
  background: rgba(89, 195, 220, 1);
  /* cursor: pointer; */
  cursor: default;
  }
  .content{
  margin-top: 0.22rem;
color: rgba(255, 255, 255, 1);
    height: 2.9rem;
    width: 100%;
  }
</style>