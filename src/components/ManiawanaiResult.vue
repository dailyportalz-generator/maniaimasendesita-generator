<template>
  <div class="maniawanai-result">
    <div class="maniawanai-result_main">
      <img src="@/assets/waku_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>
        <div class="maniawanai-result__message">
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span
                  :key="result"
                  v-if="questions[`q${questionNumber+1}`] === resultIndex+1"
                >{{result}}</span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/waku_left.gif" alt>
      </div>
      <img src="@/assets/waku_down.gif" alt>
    </div>
  </div>
</template>

<script>
import { stringify } from "querystring";
export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    resultsList() {
      return [
        [
          "ご依頼いただいていた件ですが、予定していた期日に間に合わなくなってしまいました。",
          "このようなお知らせをすることをお許しください。ご依頼の件、期日の完成が難しい状況です。",
          "悲しい知らせがあります。例の件……、まにあいそうにもないのです。",
          "さきほど電話をさしあげたのですが、いらっしゃらないようでしたのでメールします。先日の件、遅れてしまいそうです。"
        ],
        [
          "しかしながら、現在 90%の完成度ですので、チェック含めてあと１日もあれば完了する見込みです。",
          "で、現在の進捗状況ですが、ほぼ９割できております。ただ、その後のチェックと修正の時間を考えますと、来週には確実かと思います。",
          "しかし、現在、おおかた完成の見通しがついております。今後の作業状況など見ながらはっきりした期日が分かりしだいご連絡いたします。",
          "でも、だいたいの骨子はできております。作業してゆくなかで若干の不安要素はありますが、さほど時間はかからないと思います。"
        ],
        [
          "ご依頼いただいてから最大限努力してきたのですが、家族のものが病気になり十分な作業時間がとれませんでしたきょうはお休みさせてください",
          "あと少しで完了！というときにパソコンが壊れ、保存していたデータが消えてしまいました。バックアップの必要性を痛感しました。",
          "なんとか期日にまにあうようにがんばっていたのですが、気分転換に出かけた散歩の途中、なんだかどうでもよくなって１日休んでしまいました。",
          "深夜に作業中、仮眠してところ５時でした。さあ作業再開！と思ったら夕方の５時でした。15時間も寝てたわけで、どうりで妙にすっきりしてました。"
        ],
        [
          "このたびはご迷惑をおかけしました。重ね重ねお詫び申し上げます。あとは精一杯やるだけです。",
          "すいませんでした。でも、このような状況で力を発揮するタイプですので、ご期待いただければと思います。",
          "お手数かけます。「終わらない仕事はない」といいますのでいつかは終わると思います。",
          "すいません。私のいとこが似たような仕事をしておりまして、そのいとこを紹介させていただいてもいいでしょうか。"
        ],
        [
          "不明な点がありましたらいつでもお電話ください（夜中でもかまいません）。",
          "ほんとうにすいませんでした。終わったら飲みに行きましょう！おごります。",
          "終わってないですけど……、とりあえず飲みますか！",
          "ああ！やっぱだめだ。すいません。もう探さないでください（携帯は壊しました）。"
        ]
      ];
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, "");
    }
  }
};
</script>

<style scoped>
img {
  user-select: none;
}
.maniawanai-result {
  width: 526px;
  margin: 0 auto;
}
.maniawanai-result_main {
  font-size: 0;
}
.maniawanai-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}
.maniawanai-result__message p:first-child {
  margin-top: 0;
}
.maniawanai-result_build {
  text-align: right;
}
.maniawanai-result_share {
  font-size: 12px;
}
.maniawanai-result_shareurl {
  width: 100%;
}
.maniawanai-result_share {
  display: flex;
  align-items: center;
}
input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>
