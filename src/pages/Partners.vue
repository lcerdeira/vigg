<template>
  <q-page class="column">
    <div class="column col-grow my-bg">
      <div
        class="col-grow column"
        :class="$q.platform.is.mobile ? 'q-py-md' : 'q-py-xl'"
      >
        <div class="column col-grow no-wrap col-grow">
          <div class="full-height col-grow column items-center justify-center">
            <carousel-3d :controls-prev-html="'&#10092; '" :controls-next-html="'&#10093;'" :clickable="false" :bias="'right'" :disable3d="true" ref="mycarousel" :controls-visible="true" :width="'300px'" :height="'410px'" :space="350" class="column justify-center col-grow" @before-slide-change="onBeforeSlideChange">
              <slide class="my-slide bg-transparent" :index="index" v-for="(member, index) in partners" :key="member.toString()+index">
                <div class="full-height full-width justify-end column">
                  <q-card class="my-card full-width justify-end column" style="height: 350px; position: absolute">
                    <q-card-section class="column justify-start no-wrap" style="height: 290px">
                      <q-card-section class="text-center column items-center q-pt-none q-px-none" :class="'full-width'">
                        <div class="full-width column justify-center content-left">
                          <a :href="member.link" target="_blank" class="text-left member-name text-black q-pb-sm row no-wrap items-start">
                            {{member.name}}
                            <q-icon size="12px" color="primary" name="eva-external-link-outline"/>
                          </a>
                        </div>
                        <div v-if="member.name2 != ''" class="full-width column justify-center content-left">
                          <a :href="member.link2" target="_blank" class="member-name text-black q-pb-sm row no-wrap items-start">
                            {{member.name2}}
                            <q-icon size="12px" color="primary" name="eva-external-link-outline"/>
                          </a>
                        </div>
                      </q-card-section>
                      <q-card-section class="text-justify column items-center q-pa-none" :class="'full-width'">
                        <p class="q-ma-none q-pb-sm">{{member.description}}</p>
                      </q-card-section>
                    </q-card-section>
                  </q-card>
                  <div class="full-width full-height column justify-start items-center">
                    <q-avatar :size="'120px'" style="position: absolute" class="shadow-2 bg-white">
                      <img :src="'partners/' + member.image">
                    </q-avatar>
                  </div>
                </div>
              </slide>
            </carousel-3d>
            <div class="row justify-around" style="width: 200px">
              <q-btn class="q-mb-md" :class="currentIndex == b ? 'btn-current': 'btn-not'" round v-for="(btn, b) in partners.length" :key="btn+b" size="5px" @click="goToSlide(b)"></q-btn>
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>

const partners = [
  { name: 'Dr. Dominic Kwiatkowski', name2: '', link: 'https://www.sanger.ac.uk/person/kwiatkowski-dominic/', link2: '', image: 'sanger.jpg', description: 'Through this collaboration we leverage the power of next-generation sequencing technologies to address aspects of the biology of Anopheles gambiae that impact upon the sustainable control of malaria.' },
  { name: 'Dr. Eric Ochomo', name2: 'Dr. Ben Abong’o', link: 'https://www.kemri.org/cghr-staff/#1571147896050-de94dc00-cfd2', link2: 'https://www.kemri.org/cghr-staff/#1580926897769-d285238f-ea32', image: 'kemri.png', description: 'Together we work on a range of basic and translational science projects including vector control trials and machine learning approaches for identifying insecticide resistant variants in genomic and transcriptomic data sets.' },
  { name: 'Dr. Luigi Sedda', name2: '', link: 'https://www.lancaster.ac.uk/health-and-medicine/about-us/people/luigi-sedda', link2: '', image: 'lancaster.png', description: 'The development of spatially explicit sampling frameworks for vectors including adaptive sampling.' },
  { name: 'Dr. Catherine Moyes', name2: 'Dr. Penny Hancock', link: 'https://www.bdi.ox.ac.uk/Team/catherine-moyes', link2: 'https://www.bdi.ox.ac.uk/Team/penny-hancock', image: 'bigdata.jpg', description: 'They lead a collaboration on geospatial modelling of insecticide resistance.' },
  { name: 'Dr. Moses Kamya', name2: '', link: 'https://chs.mak.ac.ug/content/moses-r-kamya', link2: '', image: 'makerere.jpg', description: 'Our major collaboration is the LLINEUP trial of next generation insecticide treated bednets.' },
  { name: 'Dr. Sarah Staedke', name2: '', link: 'https://www.lshtm.ac.uk/aboutus/people/staedke.sarah', link2: '', image: 'lshtm.png', description: 'Our major collaboration is the LLINEUP trial of next generation insecticide treated bednets.' },
  { name: 'Dr. Luc Djogbenou', name2: '', link: 'https://www.researchgate.net/profile/Luc_Djogbenou', link2: '', image: 'abomi.png', description: 'He is a Professor and Wellcome Trust Fellow based at the Institut Régional de Santé Publique/University of Abomey-Calavi. His fellowship addresses the interaction between insecticide resistance and vectorial ability in Anopheles gambiae.' }
]

import { Carousel3d, Slide } from 'vue-carousel-3d'
import { openURL } from 'quasar'

export default {
  name: 'Partners',
  components: { Carousel3d, Slide },
  data () {
    return {
      partners,
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
    text-decoration: none;
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
