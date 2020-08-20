<template>
    <div>
        <div class="container">
            <div class="wrap">
                <div ref="firstHourNumWrap" class="first-num-wrap">
                    <p v-for="item of firstNumRange2" :key="item" :class="{active:firstHour===item}">{{item}}</p>
                </div>
                <div ref="lastHourNumWrap" class="last-num-wrap">
                    <p v-for="item of lastNumRange" :key="item" :class="{active:lastHour===item}">{{item}}</p>
                </div>
            </div>
            <div class="wrap">
                <div ref="firstMinuteNumWrap" class="first-num-wrap">
                    <p v-for="item of firstNumRange1" :key="item" :class="{active:firstMinute===item}">{{item}}</p>
                </div>
                <div ref="lastMinuteNumWrap" class="last-num-wrap">
                    <p v-for="item of lastNumRange" :key="item" :class="{active:lastMinute===item}">{{item}}</p>
                </div>
            </div>
            <div class="wrap">
                <div ref="firstSecondNumWrap" class="first-num-wrap">
                    <p v-for="item of firstNumRange1" :key="item" :class="{active:firstSecond===item}">{{item}}</p>
                </div>
                <div ref="lastSecondNumWrap" class="last-num-wrap">
                    <p v-for="item of lastNumRange" :key="item" :class="{active:lastSecond===item}">{{item}}</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
      data(){
        return{
          firstNumRange1:[0,1,2,3,4,5],
          lastNumRange:[0,1,2,3,4,5,6,7,8,9],
          firstNumRange2:[0,1,2],
          currentDate:null,
          firstSecond:null,
          lastSecond:null,
          firstMinute:null,
          lastMinute:null,
          firstHour:null,
          lastHour:null
        }
      },
      created() {
        setInterval(()=>{
          this.currentDate = new Date()
        },1000)
      },
      watch:{
        getDateSecond(newVal){
            const secondArr = newVal.split('')
            this.firstSecond = +secondArr[0]
            this.lastSecond = +secondArr[1]
          // 监听firstSecond和5之间的距离
          const firstSecondToFive = this.firstSecond-5
          this.$refs.firstSecondNumWrap.style.top = -(22.8*firstSecondToFive)+'px'
          // 监听lastSecond和5之间的距离
          const lastSecondToFive = this.lastSecond-5
          this.$refs.lastSecondNumWrap.style.top = -(22.8*lastSecondToFive)+'px'
        },
        getDateMinute(newVal){
          const minuteArr = newVal.split('')
          this.firstMinute = +minuteArr[0]
          this.lastMinute = +minuteArr[1]
          // 监听firstMinute和5之间的距离
          const firstMinuteToFive = this.firstMinute-5
          this.$refs.firstMinuteNumWrap.style.top = -(22.8*firstMinuteToFive)+'px'
          // 监听lastMinute和5之间的距离
          const lastMinuteToFive = this.lastMinute-5
          this.$refs.lastMinuteNumWrap.style.top = -(22.8*lastMinuteToFive)+'px'
        },
        getDateHour(newVal){
          const hourArr = newVal.split('')
          this.firstHour = +hourArr[0]
          this.lastHour = +hourArr[1]
          // 监听firstHour和5之间的距离
          const firstHourToFive = this.firstHour-5
          this.$refs.firstHourNumWrap.style.top = -(22.8*firstHourToFive)+'px'
          // 监听lastHour和5之间的距离
          const lastHourToFive = this.lastHour-5
          this.$refs.lastHourNumWrap.style.top = -(22.8*lastHourToFive)+'px'
        }

      },
      computed:{
        getDateSecond(){
          if(this.currentDate){
            return this.currentDate.getSeconds().toString().padStart(2,'0')
          }else {
            return ''
          }
        },
        getDateMinute(){
          if(this.currentDate){
            return this.currentDate.getMinutes().toString().padStart(2,'0')
          }else {
            return ''
          }
        },
        getDateHour(){
          if(this.currentDate){
            return this.currentDate.getHours().toString().padStart(2,'0')
          }else {
            return ''
          }
        }

      }

    }
</script>
<style lang="scss" scoped>
    .container{
        position: absolute;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        font-size: 10px;
        color: #ddd;
        display: flex;
        .wrap{
            position: relative;
            width: 30px;
            display: flex;
            margin-right: 15px;
            &::after{
                content: "";
                display: block;
                clear: both;
            }
            .first-num-wrap{
                position: absolute;
                top:0;
                left:0;
                transition: all 1s ease;
            }
            .last-num-wrap{
                position: absolute;
                top:0;
                right:0;
                transition: all 1s ease;
            }
            .active{
                color:#666;
            }
        }


    }
</style>
