<template>
  <q-page class="q-px-md row justify-center">
    <div
      class="my-bg"
      :class="$q.platform.is.mobile ? 'col-11 q-py-md' : 'col-10'"
      style="max-width: 1000px"
    >
      <q-carousel
        :class="$q.platform.is.mobile ? 'q-mt-md' : ''"
        swipeable
        animated
        v-model="slide"
        thumbnails
        infinite
        :height="$q.platform.is.mobile ? '170px' : ''"
      >
        <q-carousel-slide class="" :name="index" :img-src="'about/'+info.image" v-for="(info, index) in projects" :key="index+'about'"/>
      </q-carousel>
      <div
        class="col-12 rounded-borders justify-center column my-content text-justify items-center"
        :class="$q.platform.is.mobile ? 'q-pa-md' : 'q-pa-lg '"
      >
        <h6
          class="q-mx-lg text-weight-bold"
          :class="$q.platform.is.mobile ? 'q-mb-md q-mt-xs' : 'q-mb-lg q-mt-xs'"
        >
          {{projects[slide].title}}
        </h6>
        <div>{{projects[slide].content}}</div>
      </div>
      <!-- <div class="row" v-for="(info, index) in projects" :key="index+'about'">
        <div class="my-img text-subtitle2 row full-width">
          <div
            class="justify-center column items-center"
            :class="'col-12'"
          >
            <q-img
              class="q-my-md"
              :height="'200px'"
              :src="'about/' + info.image"
            >
              <div class="absolute-bottom text-subtitle1 text-center">
                {{info.title}}
              </div>
            </q-img>
          </div>
          <div
            class="q-pa-lg rounded-borders justify-center column my-content text-justify"
            :class="'col-12'"
          >
            {{info.content}}
          </div>
        </div>
      </div> -->
    </div>
  </q-page>
</template>

<script>

const projects = [
  {
    title: 'LLINEUP',
    content: 'One of the largest ever trials of vector control tools is ongoing in Uganda; the LLIN Evaluation in Uganda Project (LLINEUP) is employing an innovative study design, embedding a randomised controlled trial within a routine bednet distribution campaign to evaluate the public health value of nets containing the traditional pyrethroid insecticides plus the synergist piperonyl butoxide (PBO). The scale of the trial affords  a unique opportunity to evaluate PBO nets across different epidemiological settings. The large-scale trial embedded within could be a paradigm for future assessment of malaria control interventions.  It may also help inform national policy on bednet use.',
    image: 'about1.jpg'
  },
  {
    title: 'GAARD',
    content: 'The GAARD project brings together a consortium of researchers from institutes in SSA and Europe.The unifying theme of this project is to exploit the power of whole genome sequencing to identify genes/regulatory regions that are associated with insecticide resistance. We use a combination of approaches including computer-based searches of existing genome data bases; large scale collections and resistance screening of malaria mosquitoes in both East and West Africa, and laboratory crossing experiments to identify rare, resistance-associated variants.',
    image: 'about2.jpg'
  },
  {
    title: 'CEASE',
    content: 'The collaboration will describe the current distribution of the mosquito and route of introduction using mosquito sampling, genetic ancestry analysis and spatial modelling, while also determining whether Anopheles stephensi is associated with increased malaria using health system data, prospective studies to identify malaria cases, and mathematical modelling. In addition, they will identify social and ecological factors which influence the distribution of Anopheles stephensi and define and trial the most appropriate mosquito control strategies.',
    image: 'about3.jpg'
  },
  {
    title: 'DRC',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam vulputate tellus ac auctor fringilla. Integer convallis sem quis magna rutrum vehicula. Donec volutpat, quam non facilisis tempus, neque leo sollicitudin dui, quis sollicitudin risus nibh at turpis.',
    image: 'about4.jpg'
  },
  {
    title: 'Tsetse genomics',
    content: 'The project will use whole-genome sequencing (WGS) data to calculate effective population size from pre- and post-intervention collections of tsetse, thus providing an estimate of the effectiveness of control methods. These data will also be used to apply methods that calculate historic population size based on WGS data to investigate past population dynamics. This will provide a better understanding of the history of tsetse populations in intervention areas, while also providing signals of the effectiveness of interventions.  The results will contribute directly to development and application of novel methods to monitor the impact of vector control programmes carried out by the Trypa-NO! and Tryp-Elim partnerships.',
    image: 'about5.jpg'
  },
  {
    title: 'Machine Learning',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam vulputate tellus ac auctor fringilla. Integer convallis sem quis magna rutrum vehicula. Donec volutpat, quam non facilisis tempus, neque leo sollicitudin dui, quis sollicitudin risus nibh at turpis. Aenean vel mollis ligula, at commodo felis. Donec convallis ac eros quis feugiat. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum condimentum ex mattis, luctus metus sed, iaculis mi. Vivamus maximus ac massa at varius',
    image: 'about5.jpg'
  }
]

export default {
  name: 'Projects',
  data () {
    return {
      projects,
      slide: 0
    }
  }
}
</script>

<style lang="scss" scoped>
  .my-bg{
    background-color: rgba(255, 255, 255, 0.9);
  }
</style>
