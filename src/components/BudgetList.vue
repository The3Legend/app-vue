<template>
  <div class="budget-list-wrap">
    <el-button type="primary" round @click="onCLicked1">Outcome</el-button>
    <el-button type="success" round @click="onCLicked2">Income</el-button>
    <el-button type="warning" round @click="onCLicked3"> Show all</el-button>
    <ElCard :header="header">
      <template v-if="isEmpty">
        <div
          ref="olo"
          class="list-item"
          v-for="(item, prop) in list"
          :key="prop"
        >
          <span class="budget-coment">{{ item.comment }}</span>
          <span
            v-if="item.value > 0"
            :style="{ color: 'green' }"
            class="budget-value off"
            >{{ item.value }}</span
          >
          <span v-else :style="{ color: 'red' }" class="budget-value on">{{
            item.value
          }}</span>
          <i
            v-if="item.value > 0"
            :style="{ color: 'green' }"
            class="el-icon-top"
          ></i>
          <i v-else class="el-icon-bottom" :style="{ color: 'red' }"></i>
          <ElButton
            type="danger"
            size="mini"
            @click="deleteItem(item.id)"
            icon="el-icon-delete"
            >Delete</ElButton
          >
        </div>
      </template>
      <ElAlert v-else type="info" :title="isTitle" :closable="false" />
    </ElCard>
  </div>
</template>
<script>
export default {
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    header: "Budget List",
    isTitle: "Empty List",
  }),
  computed: {
    isEmpty() {
      return Boolean(Object.keys(this.list).length);
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    onCLicked1() {
      this.$refs.olo.forEach((el) => {
        if (el.children[1].innerText < 0) {
          el.setAttribute("style", "display: block");
          el.setAttribute("style", "margin: auto");
        } else el.setAttribute("style", "display: none");
      });
    },

    onCLicked2() {
      this.$refs.olo.forEach((el) => {
        if (el.children[1].innerText > 0) {
          el.setAttribute("style", "display: block"),
            el.setAttribute("style", "margin: auto");
        } else el.setAttribute("style", "display: none");
      });
    },
    onCLicked3() {
      this.$refs.olo.forEach((el) => {
        el.children[1].innerText < 0,
          el.setAttribute("style", "display: block");
        el.setAttribute("style", "margin: auto");
      });
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  width: 500px;
  margin: auto;
}
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
