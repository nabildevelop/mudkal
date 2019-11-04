<template>
  <div class="main-card">
    <div class="header">
        <div class="title">مدرب الكلمات</div>
        <div class="score">النتيجة: 0</div>
    </div>
    <div v-if="question!=null" class="q-panel">
      <div class="question">
        ما هي الكلمة الشبيهة بـ {{question.word}} ؟
      </div>
      <div class="option-container" v-for="(option,i) in question.options" :key="i">
        <div class="option" @click="select(i)"
          :class="{optioncorrect: question.userChoice==i&&question.value, optionincorrect: question.userChoice==i&&question.value==false}">
          {{option}}
          <span v-if="question.userChoice==i">
            <img v-if="question.value" class="option-icon" src="../assets/check-solid.svg"/>
            <img v-if="question.value==false" class="option-icon" src="../assets/times-solid.svg"/>
          </span>
        </div>
        <div v-if="i==0" class="or">
          أو
        </div>
      </div>
    </div>
    <div class="score-marks">
      <div v-for="(question, i) in questions" :key="i" class="score-mark"
        :class="{scoremarkcorrect: question.value, scoremarkincorrect: question.value==false}"/>
    </div>
  </div>
</template>

<script>
const d = require('../data/1.json')
export default {
  created(){
    /* eslint-disable no-console */
    console.log(d);
    console.log("d has a length of: "+d.length)
    /* eslint-enable no-console */

    this.questions = d.map((a)=>this.questenify(a))
  },
  data(){
    return {
      questions: null,
      corrected: false,
      userChoice: -1,
      marks: [null, null, null, null, null],
      currentIndex: 0,
    }
  },
  computed:{
    question: function(){
      return this.questions[this.currentIndex]
    }
  },
  methods:{
    questenify(arr){
      return {
        word: arr[0],
        options: arr.slice(1,3),
        correct: arr[3],
        userChoice: null,
        value: null,
      }
    },
    select(i){
      if(this.question.userChoice==null){
        this.question.userChoice = i
        this.question.value = this.question.userChoice==this.question.correct
        setTimeout(()=>{
          this.currentIndex++
        }, 1000)
      }
    },
  }
}
</script>

<style scoped>
.main-card{
    padding: 8px;
    border-radius: 8px;
    box-shadow: 0px 0px 6px #444444;
    max-width: 600px;
    margin: auto;
    display: flex;
    flex-direction: column
}
.header{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
.title{
    color: blue;
    font-weight: bold;
}
.option{
  border: 1px #888888 solid;
  margin-top: 12px;
  border-radius: 4px;
  padding: 8px;
}

.option:hover{
  cursor:pointer;
}

.optioncorrect{
  background: rgb(0, 61, 0);
  color: white;
  border: 1px rgb(0, 61, 0) solid;
}
.optionincorrect{
  background: rgb(184, 1, 1);
  color: white;
  border: 1px rgb(184, 1, 1) solid;
}
.or{
  margin-top: 12px;
  color: #888888;
}
.score-marks{
  display: flex;
  padding: 8px;
  justify-content: center;
  margin-top: 8px;
}
.score-mark{
  background: #AAAAAA;
  height: 12px;
  width: 12px;
  margin-right: 2px;
  margin-left: 2px;
  border-radius: 12px;
}
.scoremarkcorrect{
  background:rgb(0, 61, 0);
}
.scoremarkincorrect{
  background:rgb(184, 1, 1);
}
.option-icon{
  height: 12px;
  width: 12px;
}
</style>