<template>
  <q-page class="column">
    <div class="column col-grow my-bg">
      <div
        class="col-grow column"
        :class="$q.platform.is.mobile ? 'q-py-md' : 'q-py-xl'"
      >
        <div class="column col-grow no-wrap col-grow">
          <div class="full-height col-grow column items-center justify-center">
            <carousel-3d :controls-prev-html="'&#10092; '" :controls-next-html="'&#10093;'" :clickable="false" :bias="'right'" :disable3d="true" ref="mycarousel" :controls-visible="true" :width="'275px'" :height="'350px'" :space="350" class="column justify-center col-grow" @before-slide-change="onBeforeSlideChange">
              <slide class="my-slide bg-transparent" :index="index" v-for="(member, index) in teamMembers" :key="member.toString()+index">
                <q-card v-if="member.name != ''" class="my-card full-height">
                  <q-card-section class="full-height column justify-center no-wrap">
                    <q-card-section class="text-center column items-center q-pt-none" :style="{width: '220px'}" :class="'full-width'">
                      <q-avatar :size="'120px'" class="my-avatar">
                        <img v-if="member.image != ''" :src="'team/' + member.image">
                        <img v-else :src="'defaultProfile.jpg'">
                      </q-avatar>
                      <div class="full-width column justify-center content-center">
                        <p class="member-name text-black">{{member.name}}</p>
                      </div>
                      <a class="row no-wrap items-center q-pt-md cursor-pointer my-link full-width" :href='member.link' target="_blank">
                        <div class="column justify-center">
                          <q-img :src="'team/' + member.logo1" :height="'30px'" :width="'30px'" />
                        </div>
                        <p class="member-info q-pl-sm text-left">{{member.info}}</p>
                      </a>
                      <a v-if="member.info2 != ''" class="row no-wrap items-center q-pt-md cursor-pointer my-link full-width" :href='member.link' target="_blank">
                        <div class="column justify-center">
                          <q-img :src="'team/' + member.logo2" :height="'30px'" :width="'30px'" />
                        </div>
                        <p class="member-info q-pl-sm text-left">{{member.info2}}</p>
                      </a>
                    </q-card-section>
                    <div class="row q-pt-xs col-grow items-end justify-around">
                      <div v-for="(social, b) in member.social" :key="social+b">
                        <q-btn @click="member.social[b] != '' ? openURL(member.social[b]) : ''" class="my-social-btn" unelevated round size="13px">
                          <q-icon style="width: 22px; height: 22px" :name="socialIcons[b]"></q-icon>
                        </q-btn>
                      </div>
                    </div>
                  </q-card-section>
                </q-card>
              </slide>
            </carousel-3d>
            <div class="row justify-around" style="width: 290px">
              <q-btn class="q-mb-md" :class="currentIndex == b ? 'btn-current': 'btn-not'" round v-for="(btn, b) in teamMembers.length" :key="btn+b" size="5px" @click="goToSlide(b)"></q-btn>
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>

const socialIcons = [
  'img:social/social1.png',
  'img:social/social2.png',
  'img:social/social3.png',
  'img:social/social4.png'
]

const teamMembers = [
  { name: 'Alison Reynolds', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', 'https://twitter.com/AliReyUK'], link: 'https://www.lstmed.ac.uk/about/people/alison-reynolds', link2: '', image: 'member8.png', logo1: 'lstm.png', logo2: '' },
  { name: 'Amy Lynd', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0001-6054-0525', 'https://scholar.google.nl/citations?hl=pt-BR&user=SOMqxUoAAAAJ', ''], link: 'https://www.lstmed.ac.uk/about/people/dr-amy-lynd', link2: '', image: 'member4.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Daniel McDermott', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', 'https://twitter.com/damcderm'], link: 'https://www.lstmed.ac.uk/about/people/daniel-mcdermott', link2: '', image: 'member11.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'David Weetman', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0002-5820-1388', 'https://scholar.google.nl/citations?hl=pt-BR&user=lS24F7sAAAAJ', 'https://twitter.com/DaveW43883848'], link: 'https://www.lstmed.ac.uk/about/people/dr-david-weetman', link2: '', image: 'member5.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Emma Reid', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0003-1552-9209', '', ''], link: 'https://www.lstmed.ac.uk/about/people/emma-reid', link2: '', image: 'member7.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Eric Lucas', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0003-3892-1668', '', 'https://twitter.com/EricRLucas'], link: 'https://www.lstmed.ac.uk/about/people/dr-eric-lucas', link2: '', image: 'member2.jpeg', logo1: 'lstm.png', logo2: '' },
  { name: 'Jessica Lingley', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', ''], link: 'https://www.lstmed.ac.uk/about/people/jessica-lingley', link2: '', image: '', logo1: 'lstm.png', logo2: '' },
  { name: 'Kirsten Duda', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', ''], link: 'https://www.lstmed.ac.uk/about/people/kirsten-duda', link2: '', image: 'member10.png', logo1: 'lstm.png', logo2: '' },
  { name: 'Louise Cerdeira', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0002-4495-2615', 'https://scholar.google.nl/citations?user=O2dcz5MAAAAJ&hl=pt-BR', 'https://twitter.com/lcerdeira', 'https://github.com/lcerdeira'], link: 'https://www.lstmed.ac.uk/', link2: '', image: 'member1.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Luciene Salas Jennings', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', ''], link: 'https://www.lstmed.ac.uk/about/people/luciene-salas-jennings', link2: '', image: 'member6.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Martin Donnelly', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0001-5218-1497', '', 'https://twitter.com/MartinDonnelly8'], link: 'https://www.lstmed.ac.uk/about/people/professor-martin-james-donnelly', link2: '', image: 'member12.jpg', logo1: 'lstm.png', logo2: '' },
  { name: 'Naomi Dyer', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['', '', ''], link: 'https://www.lstmed.ac.uk/', link2: '', image: '', logo1: 'lstm.png', logo2: '' },
  { name: 'Sanjay Nagi', info: 'Liverpool School of Tropical Medicine', info2: '', social: ['https://orcid.org/0000-0003-1214-8523', 'https://scholar.google.nl/citations?hl=pt-BR&user=P-ImwEcAAAAJ', 'https://twitter.com/Sanjay_C_Nagi', 'https://github.com/sanjaynagi'], link: 'https://www.lstmed.ac.uk/about/people/sanjay-nagi', link2: '', image: 'member3.jpeg', logo1: 'lstm.png', logo2: '' }
]

import { Carousel3d, Slide } from 'vue-carousel-3d'
import { openURL } from 'quasar'

export default {
  name: 'Team',
  components: { Carousel3d, Slide },
  data () {
    return {
      socialIcons,
      teamMembers,
      currentSocial: 0,
      currentIndex: 0
    }
  },
  methods: {
    openURL,
    filterEmpty (socials) {
      const findEmpty = arr => arr.filter((item, index) => item === '')
      const result = findEmpty(socials)
      return result.length === this.socialIcons.length - 1
    },
    onBeforeSlideChange (index) {
      this.currentIndex = index
    },
    goToSlide (index) {
      this.$refs.mycarousel.goSlide(index)
    }
  }
}
</script>

<style lang="scss" scoped>
  .my-card{
    background-color: rgba(255, 255, 255, 0.85);
    border: 0;
  }
  .my-slide{
    border: none;
    background-color: transparent;
  }
  .member-name{
    text-transform: uppercase;
    font-weight: 600;
    letter-spacing: 3px;
    font-size: 16px;
    margin: 0;
    padding-top: 10px;
  }
  .my-link{
    color: black;
  }
  .member-info{
    color: black;
    margin: 0;
  }
  .my-social-btn{
    background-color: rgba(0, 0, 0, 0.1);
  }
  .btn-current{
    background-color: white;
    border: 1px solid white;
  }
  .btn-not{
    background-color: rgba(255, 255, 255, 0.2);
    border: 1px solid white;
  }
  ::v-deep .prev {
    color: rgba(255, 255, 255, 0.8);
  }
  ::v-deep .next {
    color: rgb(255, 255, 255, 0.8);
  }
</style>
