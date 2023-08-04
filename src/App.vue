<template>
  <div class="container">
    <transition name="fade" appear mode="out-in">
      <component
        :is="screens[position]"
        :question="question"
        :result="result"
        @goto="handleGoTo"
        @question="handleQuestion"
        @showReults="showReults"
        @startOver='startOver'
        @handleToast="handleToast"
      />
    </transition>
  </div>

  <!-- <appInitial></appInitial>
 <appConfirm></appConfirm>
 <appResults></appResults> -->
</template>

<script>
import appInitial from "./components/appInitial.vue";
import appConfirm from "./components/appConfirm.vue";
import appResults from "./components/appResults.vue";

export default {
  components: {
    appInitial,
    appConfirm,
    appResults,
  },
  data() {
    return {
      list: [
        "Yes",
        "No",
        "Maybe",
        "Not sure..try again",
        "Ask a friend",
        "Call the police",
      ],
      // this logic used to change pages in web when we are runing webpage
      screens: ["appInitial", "appConfirm", "appResults"],
      // this position variable difines which page should be opening
      position: 0,
      question: "",
      result: "",
    };
  },
  methods: {

    handleToast(values){


   this.$toast.show(values.message,{
    type:values.type,
    position:"top",
    duration:2000,
    pauseOnHover:false
   })
    },

    handleGoTo(position) {
      this.position = position;
    },
    handleQuestion(question) {
      this.question = question;
    },

    randomValue() {
      return this.list[Math.floor(Math.random() * this.list.length)];
    },

    generateResult() {
      let rand = this.randomValue();

      if (this.result !== "") {
        while (rand === this.result) {
          rand = this.randomValue();
        }
      }

      this.result = rand;
    },

    showReults() {
      this.generateResult();
    },

    startOver() {
      this.position = 0;
      this.question = "";
      this.result = "";
    },
  },
};
</script>

<style>
@import "./assets/style.css";

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: 3s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: 1s;
}
.fade-leave-to {
  opacity: 0;
}
</style>
