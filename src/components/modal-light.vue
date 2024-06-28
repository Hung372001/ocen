<script>
export default {
  name:'model-light',
  props:{
    coin:{
      type:String,
    },
    showModal:{
      type:Boolean,
      default:true
    }
  },
  emits: ['close'],
  data(){
    return{
      lv:5,
      maxlv:10,

    }
  },
  methods: {
    handleClick() {
      const newData = this.coin -1000;
      this.lv++
      this.$emit('data-change', newData);
    },
  },

}
</script>

<template>
  <div v-if="showModal">
    <div class="absolute z-10 bg-[#1A1E21] opacity-70 h-full w-full">
    </div>
    <img src="/Group%2053.png" alt="" class="left-[5px] z-10 top-[135px] absolute w-[445.43px] h-[622px]" srcset="">
    <img src="/avatar.png" class="left-[44px] absolute top-[401px] w-[90px] h-[84px] z-20">
    <div class="w-[307.48px] absolute left-[77.52px] border-white border-[1px] z-10 top-[427.16px] bg-gradient-to-r from-[#5FF9FE]  to-[#1376BD]  h rounded-full h-[31.71px] dark:bg-gray-700">
      <div class="bg-gradient-to-r from-[#A92052] via-[#F67C41] to-[#FFF051]  h-[31.71px] rounded-full" :style="{ width:(lv/maxlv)*100 +'%' }"></div>
    </div>
    <p class="text-[#CC3606] w-[139px] text-[18px] z-10 absolute left-[139px] top-[400px]">
      Level {{this.lv}}
    </p>
    <p class="text-[#CC3606] w-[139px] text-[18px] z-10 absolute left-[289px] top-[400px]">
      Claim 24/h
    </p>
    <img  @click="$emit('close')" src="/cancel.png" class="absolute top-[513px] left-[70px] w-[110px] h-[41px] z-20 "/>
    <img v-if="lv<maxlv" @click="handleClick" src="/buy.png" class="absolute top-[513px] left-[253px] w-[110px] h-[41px] z-20 "/>
  </div>
</template>

<style scoped>

</style>