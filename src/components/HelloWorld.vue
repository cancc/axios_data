<template>
  <div class="hello">
     <!-- <div class="lucy" v-for="(item, index) in Lucy" >
      <span class="lucy-name">{{item.user.nickname}}</span>
      <div class="lucy-content">{{item.content}}</div>
    </div> -->
    <div class="lucy" >
      <span class="lucy-name">{{Lucy.name}}</span>
      <div class="lucy-content">{{Lucy.content}}</div>
    </div>
    <p>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>></p>
    <!-- <button @click="next">下一页</button> -->
   
    <!-- <div class="list" v-for="(item, index) in list" >
      <span class="name">{{item.user.nickname}}</span>
      <div class="content">{{item.content}}</div>
    </div> -->
  </div>
</template>

<script>
import axios from  'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      list: [],
      limit: 100,
      offset: (1-1)*100,
      total: 1,
      page: 1,
      Lucy: {
        name: '',
        content: ''
      }
      // Lucy: []
    }
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      axios.get('/api/v1/resource/comments/R_SO_4_466369306',{
        params: {
          limit:this.limit,
          offset:this.offset,
        }
      }).then((res) => {
         // console.log(res)
          this.list = res.data.comments;
          this.total = res.data.total;
          console.log(this.total)
          //console.log(this.list);
          for(var i=0;i<this.list.length;i++) {
            if(this.list[i].user.nickname==='') {
              console.log(i, this.list[i].content);
              alert('有信息')
              this.Lucy = this.list[i];
              this.Lucy.name = this.list[i].user.nickname;
              this.Lucy.content = this.list[i].content;
              //this.Lucy.push(this.list[i]);
              //console.log(this.Lucy);
            }else if(this.offset < this.total) {
              this.page = this.page + 1;
              this.offset = (this.page-1)*100;
              this.getData();
            }
          }
        })
    },

    // next() {
    //   this.page = this.page + 1;
    //   this.offset = (this.page-1)*100;
    //   this.getData();
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.name {
  font-size: 20px;
  color: #42b983;
}
.content {
  background: #eeeeee
}
.lucy {
  border: 2px solid #eee;
  background: #ececec
}
</style>
