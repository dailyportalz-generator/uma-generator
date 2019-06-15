<template>
  <div class="result">
    <div class="result__header">
      <div class="result__container">
        <p class="orange-title">結果発表</p>
        <p>おめでとう！あなたはＵＭＡと見間違えられることに成功しました。あなたが発端で生まれたＵＭＡは、こんなＵＭＡです。</p>
      </div>
    </div>
    <div class="result__container">
      <p class="result__title">{{name}}</p>
      <div class="result__image">
        <img src="http://dpz.la.coocan.jp/20091027/img/uma3.jpg" />
        <p class="orange-title">目撃者による{{name}}の再現図。</p>
      </div>
      <h2 class="result__section-title">概要</h2>
      <p>{{name}}は猿人に似た未確認生物である。</p>
      <h2 class="result__section-title">外見</h2>
      <p>
・目は大きくつり上がっている。
・体毛の色は茶色。
・頭頂部にとさか状の飾り毛がある。
・動体視力に優れ、低空を飛んでいる鳥を捕まえることがある。
      </p>
      <h2 class="result__section-title">特徴</h2>
つい先週、アメリカのウィスコンシン州で最初に目撃された。

目撃証言のうちほとんどが、二頭で行動している。体つきなどが異なることから男女のつがいと思われるが、微妙な距離感に「まだ付き合っていないか、付き合い始めて日が浅いのでは」とする目撃者も多い。

また、高い知能を持ち、道具を使うことも知られている。特にナイフを与えると喜んで受け取り、刃を舐めるフリをするなど、程度の低い悪ノリをする。

警戒心が強く、接近しすぎると、興奮して小石や糞などを投げつけてくる。

近年、地元ではナカザンッシーを観光資源にしようという動きも盛んである。地元の観光業者によるナカザンッシーウォッチングツアーが組まれ、毎年多くの観光客が訪れている。
      <h2 class="result__section-title">正体</h2>
      <p>目撃される地域がキツネの生息地と重なっていることから、「大型のキツネの見間違いではないか」と言われている。実際にかつてナカザンッシーの声とされていた音が、専門家の解析の結果、キツネの鳴き声と判明したこともあった。 しかし、ナカザンッシーが二足歩行で歩き回っている姿も目撃されており、依然として全てが見間違いとは言い切れない。</p>
      <p></p>
      <div class="result__postscript">
        <p>このページへの直リンク</p>
        <p><a>http://</a></p>
        <p>あなたの分身であるこのＵＭＡ、その噂が一人歩きしてどんどん大ごとになっていく予感に胸を膨らませながら、平穏な日常をお過ごしください。</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    questions: Object
  },
  computed: {
    name() {
      return "ナカザンッシー"
    }
  }
}
</script>

<style scoped>
.result {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.result__container {
  width: 320px;
}
.result__header {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}
.result__title {
  font-size: x-large;
}
.result__section-title {
  font-size: x-large;
  border-bottom: 2px solid #666666;
}
.result__image {
  text-align: center;
}
.result__postscript {
  border-width: 1;
  padding: 10px;
  background-color: rgb(255, 255, 204);
}
.orange-title {
  color: orange;
  font-weight: bold;
}
</style>
