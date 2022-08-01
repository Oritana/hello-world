<template>
    <div class="container">
        <div class="clock">
            <div class="date">
                <p>{{year}}/{{month}}/{{day}}</p>
            </div>
            <div class="time">
                <p>
                    {{hours}}:{{minutes}}<span class="seconds">:{{seconds}}</span>
                </p>
            </div>
            <!-- ボタンを追加 -->
            <div class="button" v-on:click="showMessage()">   <!-- クリックしたらアラートを表示させる ここでは、showMessage()という名前にする -->
                <p>10秒後にアラームを設定</p>                   <!-- 表示したい文字を<p>タグに記述 -->
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name:"ClockScreen",
    //data()は、components内で利用できるデータを保持できるメソッド
    data(){
        return{
            //現在の日時を保持
            date:new Date(),
        };                           
    },


//computedは、data()で保持したデータを加工したい場合に利用するプロパティ
computed:{
    //年
    year(){
        return this.date.getFullYear();
    },
    //月
    month(){
        return this.date.getMonth() + 1;
    },
    //日
    day(){
        return this.dateTimePadding(this.date.getDate());  
    },
    //時
    hours(){
        return this.dateTimePadding(this.date.getHours());
    },
    //分
    minutes(){
        return this.dateTimePadding(this.date.getMinutes());
    },
    //秒
    seconds(){
        return this.dateTimePadding(this.date.getSeconds());
    },
},



    //mounted()はマウントされた後に実行され、これ以降のライフサイクルからDOM要素にアクセスが可能となる
    mounted(){
        //現在日時をセット
        this.setDate();
        //1秒ごとにsetDate()を実行                    
        setInterval(() => this.setDate(),1000); 
    },



    //methodsは、templateタグやscriptタグ内で呼び出せる関数を記載する場所
    methods:{
        //日時を二桁に変換
        dateTimePadding(num){              //関数名()
            return("0" + num).slice(-2);   //処理
        },

        //現在日時をセット
        setDate(){
            this.date = new Date(); 
        },

        //10秒後にアラートを実行
        //<template>タグ内で記述したshowMessageを記述
        showMessage(){
            window.setTimeout(() => {
                alert("10秒経過しました");    /* アラームを表示するコード */
            },10000);
        }
    },
}
</script>


<!-- scopedを記述することによって、CSSの適用範囲をこのファイルのみに指定 -->
<style scoped>   /* <template>タグ内に記述されているhtml要素を見ながらCSSを適用 */
.container {
  height: 100%;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  background-color: #262626;
}

/* pタグに「.」は不要 */
p {
  margin: 0px;
}

/* dateとtimeにCSSで文字のレイアウトを決める */
.date,
.time {
  font-weight: 700;
  color: #00ff01;
}
.date {
  font-size: 16px;
  text-align: right;
}
.time {
  font-size: 70px;
}
.seconds {
  font-size: 30px;
}
.button {
  border: 1px solid #fcfcfc;
  text-align: center;
  padding: 10px 0;
  color: #fcfcfc;
  cursor: pointer;
}
</style>