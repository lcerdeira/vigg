<template>
  <q-page class="row justify-end">
    <div class="column justify-end" style="width: 90%; max-width: 90%">
      <div
        style="paddingTop: 35px"
        :style="{height: $q.screen.width < 415 ? '175px' : '155px', marginBottom: $q.platform.is.mobile ? '200px' : '100px' }"
      >
        <div class="fade-in full-height column no-wrap">
          <div
            class="my-title"
            style="padding-bottom: 15px"
            :class="$q.screen.width < 415 ? 'column' : 'row' "
          >
            <div class="row">
              <h4
                class="q-ma-none q-pt-sm q-pl-sm text-white"
              >
                <b>Vector Informatics and Genomics Group</b>
              </h4>
            </div>
          </div>
          <div class="column items-end">
            <div class="row justify-end">
              <div class="my-tabs full-height">
                <div
                  class="full-height wrap row"
                  style="max-width: 740px"
                >
                  <div class="wrap row" style="height: 40px" v-for="(page, index) in pages" :key="index">
                    <q-btn
                      v-if="index < 5"
                      style="font-weight: bold"
                      class="full-height"
                      :style="{color:'#025B72'}"
                      :label="page"
                      @click="changePage(page)"
                      flat
                    />
                    <q-btn
                      v-else
                      :icon="page == 'twitter' ? 'img:twitter.svg' : 'mail'"
                      style="font-weight: bold; color: #0384A6"
                      class="full-height"
                      @click="changePage(page)"
                      flat
                    >
                    <q-tooltip class="text-center" transition-show="rotate" transition-hide="rotate">
                      <div class="text-center">
                        {{page == 'twitter' ? 'Twitter' : 'Contact Us'}}
                      </div>
                    </q-tooltip>
                    </q-btn>
                    <q-separator v-if="index == 4" class="full-height" vertical/>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>

import { openURL } from 'quasar'

export default {
  name: 'Home',
  data () {
    return {
      pagesLinks: this.pages,
      breaks: [415]
    }
  },
  computed: {
    currentPage: {
      get () {
        return this.$store.state.vector.currentPage
      },
      set (val) {
        this.$store.commit('vector/changePage', val)
      }
    },
    pages: {
      get () {
        return this.$store.state.vector.pages
      }
    },
    openContactForm: {
      get () {
        return this.$store.state.vector.openContactForm
      },
      set (val) {
        this.$store.commit('vector/changeContact', val)
      }
    }
  },
  methods: {
    changePage (page) {
      switch (page) {
        case 'twitter':
          openURL('https://twitter.com/LSTMvector')
          break
        case 'contact us':
          this.openContactForm = true
          break
        default:
          this.currentPage = page
          break
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .my-title{
    background-color: rgba(0, 95, 119, 0.95);
  }
  .my-tabs{
    background-color: rgba(255, 255, 255, 0.65);
  }
  .fade-in {
    opacity: 1;
    animation-name: fadeInOpacity;
    animation-iteration-count: 1;
    animation-timing-function: ease-in;
    animation-duration: 1.5s;
  }

  @keyframes fadeInOpacity {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
