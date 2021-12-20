<template lang="">
  <div>
    <span
      @click="selectedTab(tab)"
      :class="{ activeTab: selectedTabItem == index }"
      class="tab"
      v-for="(tab, index) in tabs"
      :key="index"
      >{{ tab.text }}</span
    >
  </div>
  <slot></slot>
</template>
<script>
export default {
    props: ['tabs'],
    data() {
        return {
            selectedTabItem: 0,
        };
    },
    methods: {
        selectedTab(tab) {
            this.selectedTabItem = tab.index;
            this.$emit('selected-tab-content', tab)
        },
    },
    emits: ['selected-tab-content']
};
</script>
<style lang=""></style>
