<template>
  <div class="level1-page">
    <h1 class="level1-title">CAESER CIPHER</h1>
    <h3 class="level1-subtitle">
      QUES:1 Plaintext: KEYWORD and Key: 8, Ciphertext: SMGEWZL.
    </h3>
    <div class="coding-image">
      <img class="" src="../../assets/images/tab2_mod26-encodings.webp" />
    </div>

    <div class="btn-container">
      <button class="btn" @click="wrongAnswer">True</button>
      <button class="btn" @click="rightAnswer">False</button>
    </div>

    <div class="level1-contianer">
      <div>
        <RouterLink to="/HelpL1Q1">
          <img class="level1" src="../../assets/images/help-img.png" />
        </RouterLink>
      </div>
      <div @click="playAudio" class="clickable">
        <img  class="level1" src="../../assets/images/audio-img.png" />
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
        <RouterLink to="/Level1Q2">
          <img class="level1" src="../../assets/images/next-img.png" />
        </RouterLink>
      </div>
    </div>
    <Feedback v-if="showFeedbackComponent" :status="feedbackStatus" />
  </div>
</template>
<script setup>
import Feedback from "../../components/Feedback.vue";
import { ref } from "vue";
import Image from "../../components/Image.vue";
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
  router.push("/Level1Q2");
};

/* Audio */

const audioSrc = ref("./src/assets/audio/L1Q1A1.mp3"); // Replace with the actual path to your audio file
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
.level1 {
  width: 100px;
  height: 100px;
}
.coding-image {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 40px;
}
.level1-title {
  text-align: center;
  font-size: 62px;
  padding-top: 20px;
}
.level1-subtitle {
  text-align: center;
  font-size: 62px;
  margin-top: 60px;
}
.btn-container {
  width: 60%;
  margin: 40px auto;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.btn {
  border: 2px solid white;
  border-radius: 5%;
  font-size: 30px;
  padding: 7px 30px;
  margin-top: 30px;
}
.level1-contianer {
  max-width: 90%;
  margin: 0 auto;
  margin-top: 100px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.clickable {
  cursor: pointer;
}
</style>