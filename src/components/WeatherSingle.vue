<template>
  <div class="item">
    <div class="date">{{unixToHumanDate(current.dt)}}</div>
    <div class="temp">{{simplifyTemp(current.temp)}}°C</div>
    <div class="icon">
      <img v-if="current.weather?.[0]
      .icon" :src="'http://openweathermap.org/img/wn/'+current.weather?.[0].icon+'@2x.png'" alt="Ikona pogody">
    </div>
  </div>
</template>

<script>
export default {
    props: {
        current: Object
    },
    methods: {
        unixToHumanDate(unixDate){
            const dt = new Date (unixDate*1000)
            return dt.toLocaleDateString()
        },
        simplifyTemp(temp){
            if(typeof temp != "object") return temp;
            return temp.min + "°C  - " + temp.max;
        }
    }
}
</script>

<style lang="scss">
.item{
  width:fit-content;
  box-shadow:0 0 5px rgb(0, 0, 0);
  color:#fff;
  background: linear-gradient(rgb(120, 78, 78), rgb(74, 67, 67));
  border-radius:5px;
  // border:2px dashed red;
  padding:.5em;
  font-weight:bold;
  .icon{
    border-radius:5px;
    background:rgba(80, 190, 96, 0.283);
    img{
      width:100px;
      height: 100px;
    }
  }
  .temp{
    margin:.5em;
  }
}
</style> 

