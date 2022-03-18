<template>
  <div class="area-work">
    <div class="page-top">
      <h3 class="pathname">{{ pagePathName }}</h3>
      <div class="button-wrap">
        <button
            v-for="(aItem) in sColumnList"
            :key="`btn-${aItem}`"
            @click="() => clickColumnsBtn(aItem)"
            :class="{'selected': aItem === box.numOfColumns}"
        >
            {{ aItem }}
        </button>
      </div>
    </div>
    <div class="box-wrap">
      <div
        v-for="(item, idx) in box.items"
        :key="'box' + idx"
        :style="`width:${cBoxWidth}%`"
        class="box"
      >
        <p>{{ item.name }}</p>
      </div>
    </div>
  </div>
</template>
<script>
import 'scss/pages/work.scss';

export default {
  name: 'Work',
  props: {
    box: {
      type: Object,
      default() {
        return this.$store.state.ui.box;
      }
    }
  },
  data() {
      return {
          sColumnList: [1, 2, 3 ,4]
      }
  },
  computed: {
    pagePathName() {
      return 'page path: ' + this.$route.path;
    },
    cBoxWidth() {
        return 100 / this.box.numOfColumns;
    }
  },
  methods: {
      clickColumnsBtn(aNum) {
          this.$store.commit('ui/setNumOfColumns', aNum);
      }
  }
};
</script>