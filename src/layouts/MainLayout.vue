<template>
  <q-layout view="lHh Lpr lFf">
    <q-header v-if="currentPage == 'home' && $q.screen.width <= 735 || currentPage != 'home'" elevated class="column" style="height: 40px">
      <q-toolbar class="col-grow">
        <q-avatar class="full-height">
          <q-img :height="'30px'" :width="'30px'" src="icons/favicon-128x128.png"/>
        </q-avatar>

        <q-toolbar-title shrink>Vector Informatics and Genomics Group</q-toolbar-title>

        <q-space />
        <div class="row" v-if="$q.screen.width > 930">
          <div class="row" v-for="(page, index) in pages" :key="index">
            <q-btn
              v-if="index < 5"
              class="full-height"
              :style="{color:'white'}"
              :label="page"
              @click="changePage(page)"
              flat
            />
            <q-btn
              v-else
              :icon="page == 'twitter' ? 'img:twitter-white.svg' : 'mail'"
              style="color: white"
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
            <q-separator dark v-if="index == 4" vertical/>
          </div>
        </div>
        <q-btn v-else flat round dense icon="menu" class="q-mr-sm" @click="drawer = !drawer" />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="drawer"
      side="right"
      :width="200"
      :breakpoint="500"
      overlay
      bordered
    >
      <q-img style="position: absolute" class="full-height" :src="'bg/' + bgURL" ></q-img>
      <q-scroll-area class="fit my-drawer column" style="position: absolute">
        <q-list class="full-width">
          <template v-for="(page, index) in pages">
            <q-item
              :key="page+index"
              v-if="index < 5"
              clickable
              v-ripple
              @click="changePage(page)"
              :style="{backgroundColor: currentPage == page ? 'rgb(0,96,119, 0.2)' : ''}"
            >
              <q-item-section class="my-tab">
                {{ page }}
              </q-item-section>
            </q-item>
          </template>
        </q-list>
        <div class="row justify-around">
          <q-btn
            class="col-grow q-py-xs"
            style="color: #007e9e"
            v-for="social in 2" :key="social+'social'"
            :icon="social == 1 ? 'img:twitter.svg' : 'mail'"
            @click="changePage(social == 1 ? 'twitter' : 'contact us')"
            flat
          />
        </div>
      </q-scroll-area>
    </q-drawer>

    <q-footer v-if="currentPage == 'home' && $q.screen.width <= 735 || currentPage != 'home'" elevated class="column" style="height: 40px">
      <q-toolbar class="col-grow justify-center row">
        <div class="text-subtitle1"> Copyright - Vector Informatics and Genomics Group - 2021</div>
      </q-toolbar>
    </q-footer>

    <q-dialog v-model="openContactForm" persistent>
      <q-card style="width: 100%" class="q-pb-xs my-card">
        <q-card-section class="q-px-lg">
          <h6 class="my-h6">Contact Us</h6>
        </q-card-section>

        <q-form greedy ref="myForm">
          <q-card-section horizontal v-for="(input, index) in inputs" :key="input.toString()+index">
            <div class="row full-width q-gutter-x-lg q-pr-lg">
              <q-input
                v-for="(item, i) in input"
                :key="item.toString()+i"
                :rules="[val => val !== null && val !== '' || 'Field is required']"
                dense
                :label="item.label"
                v-model="item.model"
                @keyup.enter="prompt = false"
                class="col-grow my-input"
                input-class="my-input-class"
                color="grey-3"
                label-color="black">
              </q-input>
            </div>
          </q-card-section>
          <q-card-actions align="right" class="text-primary q-px-lg">
            <q-btn class="my-btn" flat label="Close" v-close-popup />
            <q-btn class="my-btn" flat label="Submit" type="submit" @click.prevent="onSubmit"/>
          </q-card-actions>
        </q-form>
      </q-card>
    </q-dialog>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

const inputs = [
  [
    {
      label: 'Company',
      model: '',
      ref: 'company'
    },
    {
      label: 'Email Address',
      model: '',
      ref: 'email'
    }
  ],
  [
    {
      label: 'First Name',
      model: '',
      ref: 'first'
    },
    {
      label: 'Last Name',
      model: '',
      ref: 'last'
    }
  ],
  [
    {
      label: 'Address',
      model: '',
      ref: 'address'
    }
  ],
  [
    {
      label: 'City',
      model: '',
      ref: 'city'
    },
    {
      label: 'Country',
      model: '',
      ref: 'country'
    },
    {
      label: 'Postal Code',
      model: '',
      ref: 'postal'
    }
  ],
  [
    {
      label: 'Additional Information',
      model: '',
      ref: 'info'
    }
  ]
]

import { openURL } from 'quasar'

export default {
  name: 'MainLayout',
  data () {
    return {
      drawer: false,
      inputs,
      bgURL: 'bg2.jpg'
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
      this.drawer = false
    },
    onSubmit () {
      this.$refs.myForm.validate().then(success => {
        if (success) {
          let body = ''
          for (let item = 0; item < this.inputs.length; item++) {
            const items = this.inputs[item]
            for (let input = 0; input < items.length; input++) {
              body = body + items[input].label + ': ' + items[input].model + '%0D%0A'
            }
          }
          openURL('mailto:lcerdeira@gmail.com?subject=Contact Us from Vector&body=' + body)
        } else {
          this.$q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'Form not Validated'
          })
        }
      })
    }
  }
}
</script>

<style lang="scss">
  body{
    font-family: 'SourceSansPro';
  }
  .my-tab{
    text-transform: capitalize;
    font-weight: 600;
    color: #007e9e;
  }
  .my-drawer{
    background-color: rgba(255, 255, 255, 0.8);
  }
  .my-h6{
    margin: 0;
    color: orange;
    font-weight: bold;
  }
  .my-btn{
    color: orange;
    font-weight: bold;
  }
  .my-input-class{
    height: 50px;
  }
  .my-card{
    background-color: rgba(255, 255, 255, 0.9);
  }
</style>
