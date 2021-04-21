<template>
  <div id="timer">
    <span style="position: absolute;
    bottom: 0;
    left: 0;">Time {{displayMinute}}:{{displaySecond}} Difficult: {{difficult}}</span>
  </div>
</template>

<script>
export default {
  name: "timer",
  props:{
    startApp:Boolean,
    firstall:Number,
  },
  data() {
    return {
      difficult: 1,
      Minute: 0,
      Second: 15,
      displayMinute: "00",
      displaySecond: "00",
      test:true,
      isEnd: false,
      all:0,
      stage:0,
    };
  },
  methods: {},
  mounted() {
    this.all = this.firstall
    this.stage = this.all / 7
    setInterval(() => {
      
      if(this.startApp ){
        if(this.all > 0){
          this.all-=1
          this.Second = this.all%60
          this.Minute = parseInt(this.all/60)
          if(this.Second < 10){
            this.displaySecond = "0"+this.Second
          }
          else{
            this.displayMinute = this.Minute
            this.displaySecond = this.Second
          }
        }
        else{
          this.isEnd = true;
          this.$emit("takeEnd",this.isEnd)
        }

        //Check for difficult
        if(this.all > this.stage * 6){
          this.difficult = 1;
          this.$emit('takeDifficult',this.difficult)
        }
        else if(this.all > this.stage * 5 && this.all <= this.stage * 6){
          this.difficult = 2;
          this.$emit('takeDifficult',this.difficult)
        }
        else if(this.all > this.stage * 4 && this.all <= this.stage * 5){
          this.difficult = 3;
          this.$emit('takeDifficult',this.difficult)
        }
        else if(this.all > this.stage * 3 && this.all <= this.stage * 4){
          this.difficult = 4;
          this.$emit('takeDifficult',this.difficult)
        }
        else if(this.all > this.stage * 2 && this.all <= this.stage * 3){
          this.difficult = 5;
          this.$emit('takeDifficult',this.difficult)
        }
        else if(this.all > this.stage * 1 && this.all <= this.stage * 2){
          this.difficult = 6;
          this.$emit('takeDifficult',this.difficult)
        }
        else{
          this.difficult = 7
          this.$emit('takeDifficult',this.difficult)
        }
        

      }
    }, 1000);
  },
};
</script>

<style></style>
