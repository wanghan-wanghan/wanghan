<template>
  <div>
    <h2>已经完成 <span id="donecount">{{num}}</span></h2>
    <ul id="donelist">
      <li :key="item.id" v-for="(item,index) in todo" v-show="item.done">
        <input type="checkbox" v-model="item.done"/>
        <p>{{item.title}}</p>
        <a href="javascript:;" @click="del(item,index)">-</a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    todo: {
      type: Array,
    },
  },
  data() {
    return {};
  },
  methods: {
      del(item, index) {
          console.log(item.id, index)
          this.$emit("del", item.id)
      }
  },
  computed: {
      num() {
          let nums = 0;
          this.todo.forEach((item) => {
              if(item.done){
                  nums++
              }
          });
          return nums;
      }
  },
};
</script>

