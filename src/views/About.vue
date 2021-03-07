<template>
  <div class="about">
    <headers @addtodo="headertodo"></headers>
    <tolist
      @del="del"
      :todo='todo'
      :to='to'
      :t="t"
    ></tolist>
    <dolist
      @del="del"
      :todo='todo'
    ></dolist>
  </div>
</template>
<script>
import headers from "../components/header";
import tolist from "../components/tolist";
import dolist from "../components/dolist";
import "../assets/style.css";
export default {
  components: {
    headers,
    tolist,
    dolist,
  },
  data() {
    return {
      todo: [],
      to: {
        a: "qwe",
        b: 2,
      },
      t: 111111111111,
    };
  },
  methods: {
    headertodo(val) {
      // 头部传过来的数据
      this.todo.push({
        id: this.setId(),
        title: val,
        done: false,
      });
    },
    setId() {
      if (localStorage.getItem("id")) {
        let id = localStorage.getItem("id");
        localStorage.setItem("id", id - 0 + 1);
        return id - 0 + 1;
      } else {
        localStorage.setItem("id", 1);
        return 1;
      }
    },
    del(val) {
      let ind = 0;
      this.todo.forEach((item, index) => {
        if (item.id == val) {
          ind = index;
          return;
        }
      });
      this.todo.splice(ind, 1);
    },
  },
};
</script>
