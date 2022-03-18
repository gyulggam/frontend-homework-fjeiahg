<template>
  <div
    v-if="pDepth < 4"
    :depth="pDepth"
    class="gnb-item"
  >
    <!-- you may make use of this component to draw gnb items -->
    <span
        v-if="cCheckExistPath"
    >
        <router-link 
            :to="pItem.pathname"
            class="link"
        >
            {{ pItem.name }}
        </router-link>
    </span>

    <span v-else>
        {{ pItem.name }}
    </span>

    <gnb-item
        v-for="(aItem, aIdx) in pItem.children"
        :key="`menu-depth${cNextDepth}-${aIdx}`"
        :pItem="aItem"
        :pDepth="cNextDepth"
    />
  </div>
</template>

<script>
export default {
  name: 'GnbItem',
  props: {
      pItem: {
          type: Object,
          default: {},
      },
      pDepth: {
          type: Number,
          default: 0
      }
  },
  computed: {
      cCheckExistPath() {
          return Object.keys(this.pItem).includes('pathname')
      },
      cNextDepth() {
          return this.pDepth + 1;
      }
  },
};
</script>
