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
        <img :src="image.url" />
        <p class="orange-title">{{image.caption}}</p>
      </div>
      <h2 class="result__section-title">概要</h2>
      <p>{{name}}は猿人に似た未確認生物である。</p>
      <h2 class="result__section-title">外見</h2>
      <ul>
        <template v-for="(feature) in features">
          <li :key="feature">{{feature}}</li>
        </template>
      </ul>
      <h2 class="result__section-title">特徴</h2>
      <p>{{q2Text}}</p>
      <p>{{q3Text}}</p>
      <p>{{q4Text}}</p>
      <p>{{q5Text}}</p>
      <p>{{q6Text}}</p>
      <h2 class="result__section-title">正体</h2>
      <p>{{q7Text}}</p>
      <p></p>
      <div class="result__postscript">
        <p>結果ページへの直リンク</p>
        <p><a :href="directUrl">{{directUrl}}</a></p>
        <p>あなたの分身であるこのＵＭＡ、その噂が一人歩きしてどんどん大ごとになっていく予感に胸を膨らませながら、平穏な日常をお過ごしください。</p>
      </div>
    </div>
    <button @click="back">戻る</button>
  </div>
</template>

<script>
import {stringify} from 'querystring';

export default {
  props: {
    questions: Object
  },
  computed: {
    nameSize() {
      return (Math.round(this.questions.s0.length / 2)) + ((this.questions.q0 + 2) + (this.questions.q1 + 3) * (this.questions.q2 + 3) + (this.questions.q3 + 5) * (this.questions.q4 + 1)) * 31
    },
    name() {
      const suffix = [
        "マン",
        "ゴン",
        "ッシー",
        "男",
        "ティ",
      ];
      return `${this.questions.s0}${suffix[this.nameSize % 5]}`
    },
    features() {
      const features = [
        "身長は２ｍ５０ｃｍを越える。",
        "目は大きくつり上がっている。",
        "脚より手の方が長い。",
        "全身が深い毛で覆われている。",
        "体毛の色は茶色。",
        "頭頂部にとさか状の飾り毛がある。",
        "足の指は4本。",
        "犬のような声で鳴く。",
        "足は速い。",
        "動体視力に優れ、低空を飛んでいる鳥を捕まえることがある。",
        "強烈な体臭を放っている",
        "体のひだを使って短い距離を滑空することがある",
        "爪に毒を持つといわれている",
        "かんきつ類を好むなど意外とさわやかな一面もある",
      ];

      // ビット文字の配列
      const bits = this.nameSize.toString(2).split("");

      // ビットが立っているやつだけ残す
      const availables = features.filter((v, i) => bits[i] === "1");

      return availables.length === 0 ? [
        "・全身が濃い灰色の体毛で覆われている<br>・身長は成人男性ほどの大きさ。"
      ] : availables;
    },
    image() {
      const baseUrl = "http://dpz.la.coocan.jp/20091027/";
      const images = [
        {url: `${baseUrl}img/uma1.jpg`, caption: `現地で撮影された${this.name}の写真。飛び跳ねる姿がよく映っている。`},
        {url: `${baseUrl}img/uma2.jpg`, caption: `森から路上に迷い出てきた${this.name}。`},
        {url: `${baseUrl}img/uma3.jpg`, caption: `目撃者による${this.name}の再現図。`},
        {url: `${baseUrl}img/uma4.jpg`, caption: `目撃者である５歳の女の子が描いた${this.name}の全身図。`},
      ];

      return images[this.nameSize % 4];
    },
    q2Text() {
      return [
        "つい先週、アメリカのウィスコンシン州で最初に目撃された。",
        "去年の6月ごろ、インド北部ウッタルプラデシュ州の村で、池に水を汲みに行った少女により目撃されたのがはじまり。",
        "1970年代の終わりごろから目撃されており、南アフリカの炭鉱夫たちの間でこの奇妙な生物の噂が広がったのが最初と思われる。",
        "生息地はドイツ北部の田舎町。元も古い記録では、16世紀のものと思われる修道士の日記に、この奇妙な生物との遭遇が書かれている。",
      ][this.questions.q0]
    },
    q3Text() {
      return [
        "目撃証言のうちほとんどが、二頭で行動している。体つきなどが異なることから男女のつがいと思われるが、微妙な距離感に「まだ付き合っていないか、付き合い始めて日が浅いのでは」とする目撃者も多い。",
        "夜行性で、目撃証言の大半が深夜に集中している。午前1時から3時頃にかけてがちょうど小腹の空く時間といわれ、部屋着のままコンビニに出かけるところが時折目撃されている。",
        "本来それほど獰猛な性格ではないといわれているが、スポーツ感覚で人を襲ったり家畜を襲ったりすることがあるため、地元では面倒くさがられている。",
        "現地では「眠る人」とも呼ばれ、目撃談の大半は寝ているところである。しかししばしば狭い橋の上やドアの前など邪魔なところで寝るため、地元では恐れられている",
        `名前は現地語で「${this.questions.s1}する人」の意。多数の目撃証言のうち8割以上が${this.questions.s1}しているところであった。このことは「学術的視点から見てもいくらなんでも${this.questions.s1}しすぎであり、それほど${this.questions.s1}する生物がいるはずがない」として、${this.name}否定派にとって格好の批判材料となっている。`,
      ][this.questions.q1]
    },
    q4Text() {
      return [
        "また、高い知能を持ち、道具を使うことも知られている。特にナイフを与えると喜んで受け取り、刃を舐めるフリをするなど、程度の低い悪ノリをする。",
        "また、知能は高くないが、しかめ面で本を読んでいるフリをするなど、知性派ぶる一面も見られる。",
        "また、他の獣と違う点として「火を恐れない」といわれる。登山者が消し忘れた焚き火の傍らで、手のひらをこすりあわせながら暖をとっていたという証言もある。",
        "また、知能は高い。棒を蟻塚に差し込み、蟻だらけになった棒を見て嫌な顔をするなど、何がしたいのかよくわからない一面もある。",
      ][this.questions.q2]
    },
    q5Text() {
      return [
        "地元の言い伝えでは新月の日に山の中で歌を歌うといわれ、その歌声を聴くと不吉なことが起こるとして恐れられている。楽しい歌も悲しい歌もコブシを利かせてネットリと歌い上げると言われている。",
        "大食漢で、しばしば人里に現れては家畜を襲うといわれているが、残さずきれいに食べるので宇宙人より行儀がいいと評判。",
        "警戒心が強く、接近しすぎると、興奮して小石や糞などを投げつけてくる。",
        `現地の言葉に、山の中で聞こえる空耳のことを「${this.name}が愚痴を言っている」という言い回しがある。`,
      ][this.questions.q3]
    },
    q6Text() {
      return [
        `近年、地元では${this.name}を観光資源にしようという動きも盛んである。地元の観光業者による${this.name}ウォッチングツアーが組まれ、毎年多くの観光客が訪れている。`,
        `近年、地元では${this.name}を観光資源にしようという動きも盛んである。地元の菓子メーカーによる${this.name}饅頭が人気を博しており、町の貴重な収入源となっている。`,
        `近年、地元では${this.name}を観光資源にしようという動きも盛んである。地元出身の歌手により、自治体に「${this.name}の歌」が寄贈された。当初はありがた迷惑と思われていたが、今ではPR活動に盛んに使われている。`,
        `近年、地元では${this.name}を観光資源にしようという動きも盛んである。半年に一度、地元の猟友会による${this.name}狩り大会が行われており、賞金目当てにたくさんのハンターが集まる。        `,
      ][this.questions.q4]
    },
    q7Text() {
      return `
目撃される地域が${this.questions.s2}の生息地と重なっていることから、「大型の${this.questions.s2}の見間違いではないか」と言われている。実際にかつて${this.name}の声とされていた音が、専門家の解析の結果、${this.questions.s2}の鳴き声と判明したこともあった。
しかし、${this.name}が二足歩行で歩き回っている姿も目撃されており、依然として全てが見間違いとは言い切れない。'`
    },
    directUrl() {
      return `https://dailyportalz.jp/kiji/uma-generator?${stringify(
        this.questions
      )}`
    }
  },
  methods: {
    back() {
      this.$emit('clear')
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
  word-break: break-all;
}
.orange-title {
  color: orange;
  font-weight: bold;
}
</style>
