<template>
  <div class="home">
    <ul>
      全选：<input
        type="checkbox"
        @change="allData"
        v-model="isCheckAll"
        :checked="isCheckAll"
      >
      <button @click="reverse">反选</button>
      <li
        v-for="(item,index) in cartData"
        :key="index"
      >
        <input
          v-model="selected"
          @change="inpCli"
          type="checkbox"
          :value="item.id"
        />
        商品ID：{{item.id}}&emsp;&emsp;
        商品名称：{{item.name}}&emsp;&emsp;
        商品价格：{{item.price}}&emsp;&emsp;
        商品数量：<button @click="left(item, index)">-</button>{{item.num}}<button @click="right(item, index)">+</button>&emsp;&emsp;
        商品小计：{{item.price * item.num}}
      </li>
    </ul>
    总计：￥{{total}}
  </div>
</template>

<script>
const arr = [
  {
    id: 1,
    name: "小米",
    price: 100,
    num: 1,
  },
  {
    id: 2,
    name: "华为",
    price: 200,
    num: 1,
  },
  {
    id: 3,
    name: "联想",
    price: 300,
    num: 1,
  },
];
export default {
  data() {
    return {
      cartData: arr,
      selected: [],
      isCheckAll: false,
      testData: [
        {
          a: "我是a",
          b: "我是b",
        },
      ],
    };
  },
  methods: {
    left(item, index) {
      if (item.num == 1) {
        confirm("机不可失，确定不要买一件吗？") &&
          this.cartData.splice(index, 1);
      } else {
        item.num--;
      }
    },
    right(item, index) {
      item.num++;
    },
    allData() {
      if (this.isCheckAll) {
        this.selected = [];
        this.cartData.forEach((item, index) => {
          this.selected.push(item.id);
        });
      } else {
        this.selected = [];
      }
    },
    reverse() {
      let arr = [];
      this.cartData.forEach((item) => {
        if (this.selected.indexOf(item.id) == -1) {
          arr.push(item.id);
        }
      });
      // // 判断全选 反选  也可以用监听
      // this.cartData.length == arr.length ? this.isCheckAll=true : this.isCheckAll = false
      this.selected = arr;
    },
    inpCli() {
      this.selected.length == this.cartData.length
        ? (this.isCheckAll = !this.isCheckAll)
        : (this.isCheckAll = false);
    },
  },
  watch: {
    selected() {
      this.selected.length == this.cartData.length
        ? (this.isCheckAll = true)
        : (this.isCheckAll = false);
    },
    // vue的深度监听
    testDataNew: {
      handler: (val, olVal) => {
        console.log("我变化了", val, olVal);
      },
      deep: true,
    },
  },
  computed: {
    // vue的深度监听
    testDataNew() {
      return JSON.stringify(this.testData);
    },
    // 总计
    total() {
      let to = 0;
      // 循环商品列表
      this.cartData.forEach((el) => {
        // 判断是否需要计算价格
        if (this.selected.includes(el.id)) {
          to += el.price * el.num;
        }
      });
      // 返回总价
      return to;
    },
  },
};
</script>
