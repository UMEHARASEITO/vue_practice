<template>
  <div class="container">
    <div>
      <p>数字を入力してください</p> 
        <el-input-number v-model="num"  :min="1" :max="100"></el-input-number>
        <!-- @clickはVueのイベントハンドリング-->
        <el-button type="primary" @click="onClick" round>送信する</el-button>
        <p id="comment">{{ comment }}</p>
        <!-- 入力した値が正解だった場合に画像を表示させるハンドリング-->
        <img id="img" :src="image" v-if="collectFlag" />
        

    </div>
  </div>
</template>

<script>
//画像フォルダに入っているデータを読み込む
import pose_aseru from '~/assets/images/pose_aseru.png'
import pose_kenasu from '~/assets/images/pose_kenasu.jpg'
import quiz_maru from '~/assets/images/quiz_maru.png'
export default {
  data() {
    return {
      //答えの数
      answer:0, 
      //チャレンジした回数
      count:0,
      //プレイヤーが入力した数
      num:0,
      //ヒント
      comment:'',
      //正解した時true
      collectFlag:false,
     //イメージファイルの格納先
     image:null,
    }
  },
  created() {
    //答えの数を設定している
   this.answer = 1 + Math.floor( Math.random() * 100 );
   console.log('正解の値' + this.answer);
  },
  methods: {
    //送信ボタンが押された時の処理
    onClick() {
      this.collectFlag = false
      //チャレンジした回数を数える
      this.count ++;
      //答えの数とプレイヤーが入力した数が一致した場合の処理
      if (this.num == this.answer) {
        this.comment = '正解!'
        if (this.count < 4 ) {
          console.log('good');
          this.image = pose_aseru  
        } else if ( this.count > 9 ) {
          console.log('soso');
          this.image = quiz_maru
        } else {
          console.log('wow')
          this.image = pose_kenasu 
        }
        this.count = 0;
        this.answer = 1 + Math.floor( Math.random() * 100 );
        this.collectFlag = true
        console.log('正解の値' + this.answer);
      //答えの数とプレイヤーが入力した数が一致しなかった場合の処理
      } else if (this.num > this.answer) {
        this.comment = '正解の値より大きいよ！'
      }　else {
        this.comment = '正解の値より小さいよ！'
      }

        
      
    }
  }
}
</script>

