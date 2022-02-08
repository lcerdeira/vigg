<template>
  <q-page class="column">
    <div
      class="col-grow column"
      style="overflow: hidden"
    >
      <q-img
        :src="'bg/' + bgURL"
        class="full-height"
        style="position: absolute"
      >
        <template v-slot:loading>
          <q-spinner-gears color="white" />
        </template>
      </q-img>
      <div class="full-height full-width" style="position: absolute">
        <q-carousel
          v-model="currentPage"
          vertical
          transition-prev="fade"
          transition-next="fade"
          animated
          class="full-height bg-transparent"
        >
          <q-carousel-slide name="home" class="q-pa-none">
            <home/>
          </q-carousel-slide>
          <q-carousel-slide name="about" class="q-pa-none">
            <about/>
          </q-carousel-slide>
          <q-carousel-slide name="projects" class="q-pa-none">
            <projects/>
          </q-carousel-slide>
          <q-carousel-slide name="publications" class="q-pa-none">
            <publications/>
          </q-carousel-slide>
          <q-carousel-slide name="team" class="q-pa-none">
            <team/>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
  </q-page>
</template>

<script>
import About from './About.vue'
import Home from './Home.vue'
import Projects from './Projects.vue'
import Publications from './Publications.vue'
import Team from './Team.vue'

export default {
  name: 'PageIndex',
  components: { Home, About, Projects, Publications, Team },
  data () {
    return {
      bgURL: 'bg2.jpg'
    }
  },
  computed: {
    currentPage: {
      get () {
        return this.$store.state.vector.currentPage
      }
    }
  }
}
</script>
