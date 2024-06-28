<script>
export default {
  name:'model-friend',
  props:{
    showModal:{
      type:Boolean,
      default:false
    },

  },
  emits: ['close'],
  methods: {
  },

}
</script>

<template>
  <div v-if="showModal">
    <div class="absolute z-10 bg-[#1A1E21] opacity-70 h-full w-full">
    </div>
    <img src="/Group%2061.png" alt="" class="left-[16px] z-10 top-[119px] absolute w-[397px] h-[593px]" srcset="">
    <img   @click="$emit('close')" src="/Union.png" class="absolute top-[170px] left-[347px] w-[39.03px] h-[39.03px] z-20 "/>
    <img src="/Group%2042.png" class="absolute left-[100px]  z-20  top-[723px] w-[241px] h-[70px]" alt="" srcset="">
  </div>
</template>

<style scoped>

</style>