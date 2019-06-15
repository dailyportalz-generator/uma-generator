<template>
  <div class="question">
    <div class="question__container">
      <div class="question__lead">
        <p><span class="orange-title">ＵＭＡに間違えられるジェネレーターです</span></p>
        <p>人魚は、昔の人がジュゴンを見間違えたことから生まれたといいます。あなただっていつ何時、そそっかしい人に見間違えられて、ＵＭＡの生みの親になってしまってもおかしくないのです。</p>
        <p>じゃあ今すぐやったろうじゃないか、というのがこのジェネレーター。いくつかの質問に答えるだけで、「あなたが正体のＵＭＡ」が勝手にできてしまうのです。やった、インターネット超便利！</p>
        <p>それではさっそく、下の質問にお答えください。質問は全部で７問です。</p>
      </div>
      <p></p>
      <form @submit.prevent="handleSubmit">
        <div class="question__item">
          <p class="orange-title">Q1.なまえを入れてください（カタカナで）</p>
          <input type="text" v-model="s0" required size="40" id="s0">
        </div>
        <div class="question__item">
          <p class="orange-title">Q2.ＵＭＡに間違えられたのはいつ？</p>
          <input type="radio" v-model="q0" :value="0" id="q0_0"><label for="q0_0">先週</label><br>
          <input type="radio" v-model="q0" :value="1" id="q0_1"><label for="q0_1">去年</label><br>
          <input type="radio" v-model="q0" :value="2" id="q0_2"><label for="q0_2">30年前</label><br>
          <input type="radio" v-model="q0" :value="3" id="q0_3"><label for="q0_3">500年くらい前</label><br>
        </div>
        <div class="question__item">
          <p class="orange-title">Q3.そのとき何してた？</p>
          <input type="radio" v-model="q1" :value="0" id="q1_0"><label for="q1_0">デート</label><br>
          <input type="radio" v-model="q1" :value="1" id="q1_1"><label for="q1_1">夜更かし</label><br>
          <input type="radio" v-model="q1" :value="2" id="q1_2"><label for="q1_2">スポーツ</label><br>
          <input type="radio" v-model="q1" :value="3" id="q1_3"><label for="q1_3">家で寝てた</label><br>
          <input type="radio" v-model="q1" :value="4" id="q1_4">
            <label for="q1_4">その他</label>&nbsp;<input type="text" v-model="s1" size="30"> していた<br>
        </div>
        <div class="question__item">
          <p class="orange-title">Q4.ところで、無人島にひとつ持っていくなら？</p>
          <input type="radio" v-model="q2" :value="0" id="q2_0"><label for="q2_0">ナイフ</label><br>
          <input type="radio" v-model="q2" :value="1" id="q2_1"><label for="q2_1">本</label><br>
          <input type="radio" v-model="q2" :value="2" id="q2_2"><label for="q2_2">マッチ／ライター</label><br>
          <input type="radio" v-model="q2" :value="3" id="q2_3"><label for="q2_3">棒</label><br>
        </div>
        <div class="question__item">
          <p class="orange-title">Q5.あなたのストレス解消法を教えて！</p>
          <input type="radio" v-model="q3" :value="0" id="q3_0"><label for="q3_0">カラオケ</label><br>
          <input type="radio" v-model="q3" :value="1" id="q3_1"><label for="q3_1">食べる</label><br>
          <input type="radio" v-model="q3" :value="2" id="q3_2"><label for="q3_2">物を投げる</label><br>
          <input type="radio" v-model="q3" :value="3" id="q3_3"><label for="q3_3">誰かに愚痴を言う</label><br>
        </div>
        <div class="question__item">
          <p class="orange-title">Q6.ご趣味はなんですか</p>
          <input type="radio" v-model="q4" :value="0" id="q4_0"><label for="q4_0">旅行</label><br>
          <input type="radio" v-model="q4" :value="1" id="q4_1"><label for="q4_1">お菓子作り</label><br>
          <input type="radio" v-model="q4" :value="2" id="q4_2"><label for="q4_2">音楽鑑賞</label><br>
          <input type="radio" v-model="q4" :value="3" id="q4_3"><label for="q4_3">キジ撃ち</label><br>
        </div>
        <div class="question__item">
          <p class="orange-title">Q7.自分を動物にたとえると？</p>
          <input type="text" v-model="s2" required size="40">
        </div>
        <p></p>
        おつかれさまでした。質問はここまでです。
        <div class="question__submit-container">
          <input type="submit" value="UMAに間違えられる！" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      s0: "", // Q1
      q0: 0, // Q2
      q1: 0, // Q3 ラジオボタン部分
      s1: "", // Q3 その他
      q2: 0, // Q4
      q3: 0, // Q5
      q4: 0, // Q6
      s2: "", // Q7
    }
  },
  methods: {
    handleSubmit() {

      if(this.s0 === ""){
  		  alert('Q1が未入力です');
      }

      if (!/^[ア-ヴ]+$/.test(this.s0)) {
        alert('Q1は全角カタカナで入力してください');
        // TODO: s0へのフォーカス
        return;
      }

      if(this.s2 === ""){
  		  alert('Q1が未入力です');
      }

      this.$emit('submit', {
        s0: this.s0, // Q1
        q0: this.q0, // Q2
        q1: this.q1, // Q3 ラジオボタン部分
        s1: this.s1, // Q3 その他
        q2: this.q2, // Q4
        q3: this.q3, // Q5
        q4: this.q4, // Q6
        s2: this.s2, // Q7
      })
    }
  }
}
</script>

<style scoped>
.question {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.question__container {
  width: 320px;
}
.question__lead {
  margin-bottom: 48px;
}
.question__item {
  margin-bottom: 48px;
}
.question__submit-container {
  padding: 16px;
  text-align: center;
}
.orange-title {
  color: orange;
  font-weight: bold;
}
</style>
