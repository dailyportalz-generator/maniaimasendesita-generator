<template>
  <div id="app">
    まにあいませんでしたメールジェネレーター
    <img alt="Vue logo" src="./assets/syachiku.jpg">

    <template>
      <span v-if="step < 5">
        <b>step{{step+1}}</b>
      </span>
      <SelectQuestion
        key="question1"
        v-if="step === 0"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />
      <SelectQuestion
        key="question2"
        v-if="step === 1"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />
      <SelectQuestion
        key="question3"
        v-if="step === 2"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 3"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 4"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
      />
      <ManiawanaiResult :step="step" :questions="questions"/>
    </template>
  </div>
</template>

<script>
import SelectQuestion from "./components/SelectQuestion.vue";
import ManiawanaiResult from "./components/ManiawanaiResult.vue";
import { parse } from "querystring";

export default {
  name: "app",
  data() {
    return {
      step: 0,
      questions: {
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1
      }
    };
  },
  components: {
    SelectQuestion,
    ManiawanaiResult
  },
  mounted() {
    const params = parse(location.search.replace("?", ""));
    const isValid = ["q1", "q2", "q3", "q4", "q5"].every(val => {
      if (!params[val]) {
        return false;
      }
      if (val != "name" && parseInt(params[val]) < 1) {
        return false;
      }
      return true;
    });
    if (isValid) {
      const questions = {
        name: params.name,
        title: parseInt(params.title),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5)
      };
      this.questions = questions;
      this.step = 5;
    }
  },
  methods: {
    handleNext() {
      this.step++;
    }
  },
  computed: {
    messageList() {
      return [
        "まにあわないことを告白しよう",
        "あとどれくらいかかりそう?",
        "どうしてできなかったのか",
        "今後の意気込みをどうぞ",
        "しめは？"
      ];
    },
    choicesList() {
      return [
        ["ノーマルに", "低姿勢に", "ドラマチックに", "いきなり嘘で"],
        ["1日あれば", "1週間あれば", "めどつかず", "実はこれから手をつける"],
        [
          "人のせいで",
          "パソコンがクラッシュ",
          "自分がクラッシュ！",
          "寝てたから"
        ],
        [
          "野球選手のように",
          "私を信頼してくださいよ",
          "他人事のように",
          "実は不安だ"
        ],
        ["まじめに", "明るく", "やっぱりやる気しない", "逃げる…"]
      ];
    }
  }
};
</script>

<style>
#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>
