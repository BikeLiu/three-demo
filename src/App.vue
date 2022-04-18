<template>
  <div>
    <select @change="handleSelect">
      <option value="1" :selected="code === '1'">1</option>
      <option value="2" :selected="code === '2'">2</option>
      <option value="3" :selected="code === '3'">3</option>
      <option value="4" :selected="code === '4'">4</option>
    </select>
    <hello-three v-if="code === '1'"></hello-three>
    <three-demo-1 v-else-if="code === '2'"></three-demo-1>
  </div>
</template>

<script>
import HelloThree from "./views/HelloThree.vue";
import ThreeDemo1 from "./views/ThreeDemo.vue";

export default {
  name: "App",
  components: {
    HelloThree,
    ThreeDemo1,
  },
  data() {
    return {
      code: "2",
    };
  },
  methods: {
    handleSelect(e) {
      this.code = e.target.value;
    },
  },
};
</script>
