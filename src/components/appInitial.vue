<template>
  <div>
    <!-- <h4>Initial Page</h4> -->
    <h1>Ask a question</h1>
    <div class="mb-3">
      <input
        name="question"
        type="text"
        class="form-control"
        id="question"
        v-model="question"
      />

      <button
        v-if="question"
        @click="handleNext"
        class="btn animate__animated animate__flip"
      >
        Next
      </button>
      <!-- <div v-if="error" class="error">Your question is to short</div> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: "",
      // error: false,
    };
  },
  methods: {
    handleNext(e) {
      e.preventDefault();

      if (this.question.length <= 5) {
        // this.error = true;
        // this.$toast.error(`Your question is to short`)
        this.$emit("handleToast", {
          type: "error",
          message: "Your question is to short",
        });
      } else if (this.question.length >= 40) {
        this.$emit("handleToast", {
          type: "error",
          message: "Your question is to long",
        });
      } else {
        this.error = false;
        //    this $emit() function help to goto anothere component(page) using main app position variable and given id(goto)
        // In this emit take two things id and variable from main app
        this.$emit("goto", 1);
        this.$emit("question", this.question);
      }
    },
  },
};
</script>
