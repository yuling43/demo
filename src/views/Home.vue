<template>
  <div>
    <ul>
      <li v-for="item in showData" :key='item.key'>
        {{item.src}}
      </li>
    </ul>
    <van-pagination 
      v-model="currentPage" 
      :total-items="totalItems" 
      :items-per-page="perItems"
      @change="onChange"
    />
  </div>
  
</template>

<script>
// @ is an alias to /src
import Vue from 'vue';
import 'vant/lib/index.css';
import { Pagination } from 'vant';
var data = []
for(let i=0;i<500;i++){
  data[i]={
    key:i,
    src:`第${i+1}张图片`
  }
}

Vue.use(Pagination);

export default {
  data() {
    return  {
      currentPage: 1,
      totalItems:500,
      perItems:100,
      totalData:data,
      showData:data.slice(0,100)
    }
  },
  methods: {
    onChange (event) {
      this.showData=[]
      setTimeout(() => {
        this.currentPage = event
        let startIndex = this.perItems*(event-1)
        let endIndex = startIndex + this.perItems
        this.showData = this.totalData.slice(startIndex,endIndex)
        console.log(this.totalData.slice(startIndex,endIndex))
      }, 10);
    }
  }
}
</script>
