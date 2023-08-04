<template>
<!-- <div>
    <h3>result</h3>
</div> -->
  <div>
    <h3>Your answer is:</h3>
    <div>
      {{ result }}
    </div>
    <div class="animate__animated animate__lightSpeedInRight animate__delay-1s">
      <hr />
      <button class="btn" @click="startOver">Start Over</button>
      <button class="btn" @click="getResult">Decide again</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["result"],
  mounted() {
    this.getResult();
  },
  methods: {
    startOver() {
      this.$emit("startOver");
    },
    getResult() {
      this.$emit("showReults");
    },
  },
};
</script>
