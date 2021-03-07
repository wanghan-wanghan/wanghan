<template>
  <div>
    <header>
      <section>
        <input
          type="text"
          id="title"
          name="title"
          placeholder="添加ToDo"
          required="required"
          autocomplete="to"
          v-model="WaitData"
          v-on:keyup.enter="enter"
        />
      </section>
    </header>
  </div>
</template>
<script>
export default {
  data() {
    return {
        WaitData:'',
    };
  },
  methods: {
      enter() {
          this.$emit("addtodo", this.WaitData);
          this.WaitData = ""
      }
  },
};
</script>