<script>
import ModelRocket from "@/components/model-rockret.vue";
import ModelLight from "@/components/modal-light.vue";
import ModelFriend from "@/components/modal-friiends.vue";
import modalMisson from "@/components/modal-misson.vue";
import ModelMisson from "@/components/modal-misson.vue";

export default {
  components: {ModelMisson, ModelFriend, ModelLight, ModelRocket},
  data() {
    return {
      coin:10000000,
      progress: 0,
      timeRemaining: 12 * 60 * 60, // Tổng số giây (12 giờ)
      interval: null,
      coinValue: 0,
      showModal: false,
      showModalLight:false,
      showMisson:false,
      showFriend:false
    };
  },
  mounted() {
    this.startProgress();
  },
  beforeUnmount() {
    clearInterval(this.interval);
  },
  computed: {
    modalMisson() {
      return modalMisson
    },
    formattedTime() {
      const hours = Math.floor(this.timeRemaining / 3600);
      const minutes = Math.floor((this.timeRemaining % 3600) / 60);
      const seconds = this.timeRemaining % 60;
      return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    },
  },
  methods: {
    startProgress() {
      this.interval = setInterval(() => {
        this.timeRemaining--;
        this.progress = ((12 * 60 * 60 - this.timeRemaining) / (12 * 60 * 60)) * 100;
        if (this.timeRemaining % 3600 === 0 && this.progress < 100) {
          this.coinValue++;
        }
        if (this.timeRemaining <= 0) {
          clearInterval(this.interval);
          this.progress = 100;
          this.timeRemaining = 0;
        }
      }, 1000);
    },
    resetProgress() {
      clearInterval(this.interval);
      this.progress = 0;
      this.coinValue = 0; // Reset giá trị coin

      this.timeRemaining = 12 * 60 * 60; // Reset về 12 giờ
      this.startProgress();
    },
    handleDataChange(newData) {
      this.coin = newData;
    },
  },
}


</script>

<template>
  <div class="flex items-center h-[100vh]">
    <div class="max-w-[430px] relative bg-[url(bg.png)]  w-full h-[932px]  my-auto mx-auto bg-no-repeat">
      <model-friend :showModal="showFriend"   @close="showFriend = false" />
      <model-misson :showModal="showMisson"   @close="showMisson = false"  />
      <model-rocket :coin="coin"   :show-modal="showModal" @close="showModal = false" @data-change="handleDataChange"/>
      <model-light :coin="coin"   :show-modal="showModalLight" @close="showModalLight = false" @data-change="handleDataChange"/>
      <div class="absolute left-[18px] z-10 top-[48px]">
           <img src="/coin.png" class="w-[51px] h-[51px] ">
      </div>
      <div class="absolute w-[104px] text-[18px] z-0 text-white rounded-[10px] bg-[#242424]  opacity-70  text-center left-[49px] top-[52px] h-[35px]">
        {{coin}}
      </div>

      <div class="absolute left-[307px] z-10 top-[34px]">
        <img src="/coin2.png" class="w-[72.14px] h-[69.36px] ">
      </div>
      <div class="absolute w-[68px] text-[18px] z-0 text-white rounded-[10px] bg-[#242424] text-center left-[341px] top-[52px] h-[35px]">
        1
      </div>
      <img @click="resetProgress" v-if="progress === 100"   src="/claim.png" class="w-[79px] h-[36px] absolute top-[237px] left-[351px] "/>
      <h1 @click="resetProgress" v-if="progress === 100" class="text-white text-[18px] w-[41px] absolute left-[377px] top-[243px]  h-[23px]">Claim</h1>
      <div class="w-[385px] absolute left-[22px] top-[620px] bg-[#1A1E21] rounded-full h-[15px] dark:bg-gray-700">
        <div class="bg-gradient-to-r from-[#A92052] via-[#F67C41] to-[#FFF051]  h-[15px] rounded-full" :style="{ width: progress + '%' }"></div>
      </div>
      <div>
        <p class="text-white text-[18px] absolute left-[22px] top-[597px]">{{formattedTime    }}</p>
        <p class="text-white text-[18px] absolute left-[341px] top-[597px]">{{coinValue    }}</p>

      </div>
      <div>
        <div>
          <img src="/rocket.png" class="left-[41px] absolute top-[700px] w-[178px] h-[112px]"/>
          <img src="/rock-btn.png" @click="showModal = true" class="left-[72px] absolute top-[765px] w-[92px] h-[34px]"/>
        </div>
        <div>
          <img src="/light.png" class="left-[234px] absolute top-[700px] w-[178px] h-[112px]"/>
          <img src="/light-btn.png"  @click="showModalLight = true" class="left-[268px] absolute top-[768px] w-[90px] h-[33px]"/>

        </div>
      </div>
      <div class="absolute border-[1px] bg-[#D9D9D9] left-[24px] top-[818px] w-[385px] h-[84px] opacity-[48%] rounded-[23px]">
      </div>
      <img @click="showMisson = true" src="/Group%2040.png"   class="absolute left-[61px] top-[828px] w-[56px] h-[63px] " />
      <img @click="showFriend = true" src="/Group%2045.png"  class="absolute left-[186px] top-[828px] w-[64px] h-[59px] " />
      <img src="/Group%2044.png" class="absolute left-[313px] top-[828px] w-[53px] h-[65px] " />
    </div>
  </div>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
