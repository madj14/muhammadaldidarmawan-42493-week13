<template>
  <div class="count">
    <v-container>
      <v-row text="center">
        <v-col align="center">
          <h2>⏱️SIMPLE COUNTDOWN⏱️</h2>
        </v-col>
      </v-row>
      <v-row>
        <v-col align="center">
          <h3 v-if="statusCount && !statusPause">Time Remaining</h3>
          <h3 v-if="statusFinish">BOOOM!!!!!</h3>
          <h3 v-if="statusPause">Time Remaining <br> Paused! </h3>
        </v-col>
      </v-row>
      <v-row>
        <v-spacer></v-spacer>
        <v-col cols="10" align="center">
          <v-row>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px" @click="tambahJam()"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px" @click="tambahMenit()"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/up-arrow.png" width="30px" @click="tambahDetik()"/></v-col>
          </v-row>
          <v-row>
            <v-col cols="3"><div>{{ displayHours || '00' }}</div></v-col>
            <v-col cols="1">:</v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><div>{{ displayMinutes || '00' }}</div></v-col>
            <v-col cols="1">:</v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><div>{{ displaySeconds || '00' }}</div></v-col>
          </v-row>
          <v-row>
            <v-col cols="3" style="padding: 0px"><span>Hours</span></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3" style="padding: 0px"><span>Minutes</span></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3" style="padding: 0px"><span>Seconds</span></v-col>
          </v-row>
          <v-row>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px" @click="kurangJam()"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px" @click="kurangMenit()"/></v-col>
            <v-spacer></v-spacer>
            <v-col cols="3"><img src="@/assets/down-arrow.png" width="30px" @click="kurangDetik()"/></v-col>
          </v-row>
          <v-row v-if="!statusCount">
            <v-col cols="12">
              <v-btn color="#C3C3C3" v-on:click="startCountdown()" dark>Start</v-btn>
            </v-col>
          </v-row>
          <v-row v-if="statusCount">
            <v-col cols="12">
              <v-btn color="#C3C3C3" style="margin: 0px 5px" v-if="statusPause" v-on:click="startCountdown()">Resume</v-btn>
              <v-btn color="#C3C3C3" style="margin: 0px 5px" @click="pauseCountdown" v-if="!statusPause" dark>Pause</v-btn>
              <v-btn color="#FF6A6A" style="margin: 0px 5px" @click="resetCountdown" v-on:click="finishCountdown()" dark>Reset</v-btn>
            </v-col>
          </v-row>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: () => ({
    displayHours: 0, displayMinutes: 0, displaySeconds: 0,
    statusCount: false, statusPause: false, statusFinish: false,
    jam: 0, menit: 0, detik: 0,
    jam1: 0, menit1: 0, detik1: 0,
    i: 0,
    pauseStats: 0,
    year: 0, month: 0, date: 0, hour: 0, minute: 0, second: 0,
  }),
  computed: {
    _detik: () => 1000,
    _menit(){
      return this._detik * 60;
    },
    _jam(){
      return this._menit * 60;
    }
  },
  methods: {
    tambahJam(){
      this.jam += 1;
      this.displayHours = this.formatNum(this.jam)
    },
    tambahMenit(){
      if (this.menit < 59) {
        this.menit += 1;
      }else{
        this.jam += 1
        this.menit = 0;
      }
      this.displayMinutes = this.formatNum(this.menit)
      this.displayHours = this.formatNum(this.jam)
      this.displaySeconds = this.formatNum(this.detik)
    },
    tambahDetik(){
      if (this.detik < 59) {
        this.detik += 1;
      }else{
        this.menit += 1
        this.detik = 0;
      }
      this.displayMinutes = this.formatNum(this.menit)
      this.displayHours = this.formatNum(this.jam)
      this.displaySeconds = this.formatNum(this.detik)
    },
    kurangJam(){
      if(this.jam > 0){
        this.jam -= 1;
      }
      this.displayHours = this.formatNum(this.jam)
    },
    kurangMenit(){
      if(this.menit > 0){
        this.menit -= 1;
      }
      this.displayMinutes = this.formatNum(this.menit)
    },
    kurangDetik(){
      if(this.detik > 0){
        this.detik -= 1;
      }
      this.displaySeconds = this.formatNum(this.detik)
    },
    startCountdown(){
      if (this.statusPause == true) {
        this.jam = this.jam1;
        this.menit = this.menit1;
        this.detik = this.detik1;
        this.statusPause = false;
      }
      if (this.jam > 0 || this.menit > 0 || this.detik > 0) {
        this.displayRemaining()
      }
    },
    formatNum: num => (num < 10 ? '0' + num : num),
    displayRemaining(){
      this.statusCount = true;
      this.statusPause = false;
      const countdown = setInterval(() => {
        const now = new Date();
        if (this.i==0) {
          this.year = now.getFullYear();
          this.month = now.getMonth();
          this.date = now.getDate();
          this.hour = now.getHours() + this.jam;
          this.minute = now.getMinutes() + this.menit;
          this.second = now.getSeconds() + this.detik;
          this.i += 1;
        }
        const end = new Date(this.year, this.month, this.date, this.hour, this.minute, this.second);
        const distance = end.getTime() - now.getTime();
        if(distance < 0){
          clearInterval(countdown);
          this.jam = 0;
          this.menit = 0;
          this.detik = 0;
          this.i = 0;
          if (this.statusPause == false) {
            this.finishCountdown();
            this.statusCount = false;
          }
          return;
        }
        const hours = Math.floor(distance / this._jam);
        const minutes = Math.floor((distance % this._jam) / this._menit);
        const seconds = Math.floor((distance % this._menit) / this._detik);
        this.jam1 = hours;
        this.menit1 = minutes;
        this.detik1 = seconds;
        this.displayHours = this.formatNum(hours);
        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
      }, 1000);
    },
    resetCountdown(){
      clearInterval(this.countdown);
      this.jam = 0; this.displayHours = this.formatNum(this.jam);
      this.menit = 0; this.displayMinutes = this.formatNum(this.menit);
      this.detik = 0; this.displaySeconds = this.formatNum(this.detik);
      this.i = 0;
      this.statusCount = false;
      this.statusPause = false;
      return;
    },
    pauseCountdown(){
      clearInterval(this.countdown);
      this.i = 0;
      this.jam = 0;
      this.menit = 0;
      this.detik = 0;
      this.statusPause = true;
      return;
    },
    finishCountdown(){
      this.statusFinish = true
      setTimeout(()=>{
        this.statusFinish = false
      }, 2000)
    }
  }
}
</script>

<style scoped>
.count{
  justify-content: center;
  align-items: center;
  display: flex;
}
</style>