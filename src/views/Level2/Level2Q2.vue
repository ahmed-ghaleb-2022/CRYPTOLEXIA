<template>
  <div class="level1-page">
    <h1 class="level1-title">VIGENERE CIPHER</h1>
    <h3 class="level1-subtitle">
      QUES:2 Plaintext: HELLO, Key: BYE, Ciphertext: .......?
    </h3>
    <div class="coding-image">
      <img class="" src="../../assets/images/vigen.png" />
    </div>
    <div class="btn-container">
      <button class="btn" @click="wrongAnswer">MPPCI</button>
      <button class="btn" @click="rightAnswer">ICPMM</button>
      <button class="btn" @click="wrongAnswer">ICMMP</button>
      <button class="btn" @click="wrongAnswer">NONE</button>
    </div>

    <div class="level1-contianer">
      <div>
        <RouterLink to="/HelpL2Q2">
          <img class="level1" src="../../assets/images/help-img.png" />
        </RouterLink>
      </div>
      <div @click="playAudio" class="clickable">
        <img class="level1" src="../../assets/images/audio-img.png" />
        <audio ref="audioElement" controls style="display: none">
          <source :src="audioSrc" type="audio/mpeg" />
          Your browser does not support the audio element.
        </audio>
      </div>
      <div>
        <RouterLink to="/">
          <img class="level1" src="../../assets/images/home-image.png" />
        </RouterLink>
      </div>

      <div>
        <RouterLink to="/Level2Q3">
          <img class="level1" src="../../assets/images/next-img.png" />
        </RouterLink>
      </div>
    </div>
    <Feedback v-if="showFeedbackComponent" :status="feedbackStatus" />
  </div>
</template>
<script setup>
import Feedback from "../../components/Feedback.vue";
import Image from "../../components/Image.vue";
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useCounterStore } from "../../stores/counter";

const route = useRoute();
const router = useRouter();
const counter = useCounterStore();




const showFeedbackComponent = ref(false);
const feedbackStatus = ref(false);

const rightAnswer = () => {
  feedbackStatus.value = true;
  counter.increment();
  showFeedback();
};

const wrongAnswer = () => {
  feedbackStatus.value = false;
  counter.decrement();
  showFeedback();
};

const showFeedback = () => {
  showFeedbackComponent.value = true;

  setTimeout(() => {
    navigateToNextPage();
  }, 3000); // 3000 milliseconds (3 seconds)
};

const navigateToNextPage = () => {
  router.push("/Level2Q3");
};




/* Audio */

const audioSrc = ref("./src/assets/audio/L2Q2A2.mp3"); // Replace with the actual path to your audio file
const audioElement = ref(null);

const playAudio = () => {
  // Check if the audio is already playing, if not, play it
  if (audioElement.value.paused) {
    audioElement.value.play();
  }
};

/* Audio */
</script>
<style scoped>
.level1-page {
  background-color: rgb(168, 230, 133);
  min-height: 100vh;
}
.coding-image {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 40px;
  margin-bottom: 30px;
}
.level1-title {
  text-align: center;
  font-size: 62px;
  padding-top: 20px;
}
.level1 {
  width: 100px;
  height: 100px;
}
.level1-subtitle {
  text-align: center;
  font-size: 62px;
  margin-top: 60px;
}
.btn-container {
  width: 60%;
  margin: 0 auto;
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-top: 20px;
}
.btn {
  border: 2px solid white;
  border-radius: 5%;
  font-size: 30px;
  padding: 7px 30px;
}
.level1-contianer {
  max-width: 90%;
  margin: 0 auto;
  margin-top: 100px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>