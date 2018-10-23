<template>
  <div class="training">
    <h1>Math training with Vue.js</h1>
    <hr />
    <p>Just a simple project with Vue.js framework.</p>
    <div class="progress">
        <div class="progress-bar" :style="progressStyles"></div>
    </div>
    <div class="box">
      <transition name="flip" mode="out-in">
          <start-screen 
            v-if="state == 'start'"
            @onStart="onStart"
          ></start-screen>
          <question 
            v-else-if="state == 'question'"
            @success="onQuestionSuccess"
            @fail="onQuestionFail"
          >
          </question>
          <message 
            v-else-if="state == 'message'"
            :type="message.type"
            :text="message.text"
            @onNext="onNext"
          ></message>
          <result-screen 
            v-else-if="state == 'result'"
            :stats="stats"
            @onStartNewGame="onStartNewGame"
          ></result-screen>
          <div v-else>Unknown state</div>
      </transition>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state: 'start',
      stats: {
        success: 0,
        error: 0
      },
      message: {
        type: '',
        text: ''
      },
      questionMax: 5
    }
  },
  computed: {
    totalQuestions(){
      return this.stats.success + this.stats.error;
    },
    progressStyles(){
      return {
        width: (this.totalQuestions / this.questionMax * 100) + '%'
      }
    }
  },
  methods: {
    onStart(){
      this.state = 'question';
    },
    onQuestionSuccess(){
      this.state = 'message';
      this.message.text = 'Good job!';
      this.message.type = 'success';
      this.stats.success++;
    },
    onQuestionFail(msg){
      this.state = 'message';
      this.message.text = 'No... ' + msg;
      this.message.type = 'danger';
      this.stats.error++;
    },
    onNext(){
      if(this.totalQuestions < this.questionMax) {
        this.state = 'question';
      } else {
        this.state = 'result';
      }
    },
    onStartNewGame(){
      this.state = 'start';
      this.stats.success = 0;
      this.stats.error = 0;
    }
  }
}
</script>

<style lang="scss" scoped>
  .box {
    margin: 10px 0;  
  }

  .training {
    max-width: 700px;
    margin: 20px auto;
  }

  .flip-enter{

  }
  .flip-enter-active{
    animation: flipInX 0.3s linear;
  }
  .flip-leave{

  }
  .flip-leave-active{
    animation: flipOutX 0.3s linear;
  }

  @keyframes flipInX {
    from{transform: rotateX(90deg);}
    to{transform: rotateX(0deg);}
  }
  @keyframes flipOutX {
    from{transform: rotateX(0deg);}
    to{transform: rotateX(90deg);}
  }
</style>
