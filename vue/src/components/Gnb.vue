<template>
  <div
    v-if="items"
    id="gnb"
  >
    <Header />
    <div class="gnb-inner">
      <!-- your code goes from here -->
      <gnb-item
        v-for="(aItem, aIdx) in items"
        :key="`menu-depth1-${aIdx}`"
        :pItem="aItem"
        :pDepth="1"
      />
    </div>
  </div>
  <div v-else>
    {{ sErrorStr }}
  </div>
</template>
<script>
import 'scss/components/gnb.scss';
import GnbItem from './GnbItem.vue'
import Header from './Header.vue'

export default {
  name: 'Gnb',
  components: {
    GnbItem,
    Header
  },
  data() {
    return {
      sampleItems: [
        {
          name: 'Menu 1',
          children: [
            {
              name: 'Menu 1-1',
              pathname: '/1-1'
            },
            {
              name: 'Menu 1-2',
              children: [
                {
                  name: 'Menu 1-2-1',
                  pathname: '/1-2-1'
                }
              ]
            }
          ]
        },
        {
          name: 'Menu 2',
          pathname: '/2'
        }
      ],
      items: null,
      sErrorStr: 'no data'
    };
  },
  methods: {
    getMenuData() {
      this.API.getGnb()
      .then(res => {
          this.items = res.data;
      })
      .catch(error => {
          this.items = null;
          console.log(error);
      });
    }
  },
  created() {
    this.getMenuData();
  }
};
</script>
