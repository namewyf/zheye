<template>
    <div class="home-page">
      <section class="py-5 text-center container">
          <div class="row py-lg-5">
              <div class="col-lg-6 col-md-8 mx-auto">
                  <img src="../assets/callout.svg" alt="callout" class="w-50"/>
                  <h2 class="font-weight-light">随心写作，自由表达</h2>
                  <router-link to="/create" class="btn btn-primary my-2">开始写文章</router-link>
              </div>
          </div>
      </section>
      <h4 class="font-weight-bold text-center">发现精彩</h4>
      <column-list :list = "list"></column-list>
    </div>
  </template>

<script lang="ts">
import { DefineComponent, defineComponent, computed } from 'vue'
import { useStore } from 'vuex'
import { GlobalDataProps } from '@/store'
import ColumnList from '@/components/ColumnList.vue'
export default defineComponent({
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',
  components: {
    ColumnList
  },
  setup () {
    const store = useStore<GlobalDataProps>()
    const list = computed(() => store.state.columns)
    const biggerColumnLen = computed(() => store.getters.biggerColumnLen)
    return {
      list,
      biggerColumnLen
    }
  }
})

</script>

  <style lang="scss" scoped>

  </style>
