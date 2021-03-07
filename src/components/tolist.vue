<template>
  <div>
    <h2>正在进行 <span id="todocount">{{num}}</span></h2>
    <ol
      id="todolist"
      class="demo-box"
    >
      <li :key="item.id" v-for="(item) in todo" v-show="!item.done">
        <input type="checkbox" v-model="item.done"/>
        <p>{{item.title}}{{cData}}</p>
        <a href="javascript:;" @click="del(item)">-</a>
      </li>
    </ol>
  </div>
</template>
<script>
export default {
  // props:['todo', 'to'],
  props: {
    todo: {
      type: Array,
    },
    // to: {
    //   type: Object,
    // },
    // t: {
    //     type: Number,
    // }
  },
  data() {
    return {
        cData:[]
    };
  },
  methods: {
      del(item) {
          console.log(item.id)
          this.$emit("del", item.id)
      }
  },

  computed: {
      num() {
          let nums = 0;
          this.todo.forEach((item) => {
              if(!item.done){
                  nums++
              }
          });
          return nums;
      }
  },
  watch: {
      todo: function(newVal,oldVal){
        
        this.cData = newVal; //newVal即是chartData
      }
    },
};
</script>