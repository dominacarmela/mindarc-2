<script>
  import json from '../assets/data.json'
  import { ref } from 'vue'

  export default{
    data(){
        return{
            myJson: json,
            myJsonSelectedContent: json[0].content
        }
    },
    methods: {
      setShowOnMobile: function(data) {
        for (let i = 0; i < json.length; i++) {
          json[i].isShowOnMobile = false
        }
        data.isShowOnMobile = !data.isShowOnMobile
        this.myJsonSelectedContent = data.content
      }
    }
  }
</script>

<template>
  <div class="mindarc-ex-2">
    <ul class="myJson-list">
      <li v-for="(data, index) in myJson"
          @click="setShowOnMobile(data, myJsonSelectedContent)"
          :class="{ 'selected' : data.isShowOnMobile}"
          class="myJson-list__item">
        <div class="myJson__title">{{data.title}}</div>
        <div v-html="data.content" class="myJson__content"></div>
      </li>
    </ul>
    <div class="myJson-selected-content" v-html="myJsonSelectedContent"></div>
  </div>
</template>

<style scoped>
.mindarc-ex-2 {
  padding: 20px;
}
.myJson-list__item {
  border-bottom: 1px solid #ccc;
  padding-bottom: 10px;
}
.myJson-list__item .myJson__content {
  visibility: hidden;
  height: 0;
  min-height: 0;
  transition: min-height 1s ease-out;
}
.myJson-list__item .myJson__title {
  padding: 10px 0 0;
}
.myJson-list__item.selected .myJson__title {
  font-weight: 700;
}
.myJson-list__item.selected .myJson__content {
  visibility: visible;
  height: auto;
  min-height: 30px;
  transition: height 1s ease-in;
}
.myJson-selected-content {
  display: none;
}

@media (min-width: 1024px) {
  .myJson-list {
    display: flex;
  }
  .myJson-list {
    position: relative;
    top: 2px;
    z-index: 9;
  }
  .myJson-list__item {
    border-bottom: 1px solid #ffffff;
    cursor: pointer;
    padding: 0;
  }
  .myJson-list .myJson__content {
    display: none;
  }
  .myJson-selected-content {
    display: block;
    padding: 10px;
    border: 1px solid #cccccc;
  }
  .myJson-list__item .myJson__title {
    padding: 10px;
  }
  .myJson-list__item.selected .myJson__title {
    font-weight: 700;
    border-right: 1px solid #cccccc;
    border-left: 1px solid #cccccc;
    border-top: 1px solid #cccccc;
    background: #ffffff;
  }
}
</style>
