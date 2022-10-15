<template>
  <div>
    <!-- Bag Image -->
    <PunchingBag :gameEnded="gameEnded" />

    <!-- Bag Health -->
    <BagHealth :state="bagHealthState" :health="bagHealthStatus" />

    <!-- Game Controls -->
    <GameControls
      :punch="handleBagPunch"
      :gameEnded="gameEnded"
      :reset="handleReset"
    />
  </div>
</template>

<script>
import PunchingBag from "./PunchingBag.vue";
import BagHealth from "./Baghealth.vue";
import GameControls from "./GameControls.vue";

export default {
  name: PunchingBag,
  components: {
    PunchingBag,
    BagHealth,
    GameControls,
  },
  data: () => ({
    bagHealthStatus: 100,
    bagHealthState: "success",
    gameEnded: false,
  }),
  methods: {
    handleBagPunch() {
      this.bagHealthState -= 10;
    },
    handleReset() {
      (this.bagHealthStatus = 100),
        (this.gameEnded = false),
        (this.bagHealthState = "success");
    },
  },
  watch: {
    bagHealthStatus(value) {
      if (value >= 30 && value <= 50) {
        this.bagHealthState = "warning";
      } else if (value < 30) {
        this.bagHealthState = "error";
      } else if (value === 0) {
        this.gameEnded = true;
      }
    },
  },
};
</script>
