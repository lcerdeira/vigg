<template>
  <q-page class="q-px-md row justify-center">
    <div
      class="q-py-md my-bg"
      :class="$q.platform.is.mobile ? 'col-11' : 'col-10'"
      style="max-width: 1000px"
    >
      <div
        class="row"
        :class="$q.platform.is.mobile ? '' : index % 2 == 0 ? 'q-pl-sm' : 'q-pr-sm'"
        v-for="(info, index) in abouts"
        :key="index+'about'"
      >
        <div class="my-img text-subtitle2 row full-width q-py-md">
          <div
            v-if="index % 2 == 0 || $q.platform.is.mobile"
            class="justify-center column items-center shadow"
            :class="$q.platform.is.mobile ? 'col-12' : 'col-4'"
          >
            <img
              :style="{width: '100%', height: '100%'}"
              :src="'about/' + info.image"
            />
          </div>
          <div
            class="q-pa-lg rounded-borders justify-center column my-content text-justify"
            :class="$q.platform.is.mobile ? 'col-12' : 'col-8'"
          >
            {{info.content}}
          </div>
          <div
            v-if="index % 2 != 0 && !$q.platform.is.mobile"
            class="col-4 justify-center column items-center shadow"
          >
            <img
              class="full-height full-width my-img"
              :src="'about/' + info.image"
            />
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>

const abouts = [
  {
    title: 'Introduction',
    content: 'A major area of interest is the evolution of insecticide resistance in the malaria mosquito Anopheles gambiae. We use a variety of approaches to identify and validate insecticide resistance associated loci.',
    image: 'about4.jpg'
  },
  {
    title: 'Team',
    content: 'Much of this work is conducted jointly with Dr David Weetman and team. A second research area is understanding the impact of insecticide resistance on malaria epidemiology ,through observational studies and randomized control trials.',
    image: 'about3.jpg'
  }
  // {
  //   title: 'Covid 19',
  //   content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam vulputate tellus ac auctor fringilla. Integer convallis sem quis magna rutrum vehicula. Donec volutpat, quam non facilisis tempus, neque leo sollicitudin dui, quis sollicitudin risus nibh at turpis. Aenean vel mollis ligula, at commodo felis. Donec convallis ac eros quis feugiat. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum condimentum ex mattis, luctus metus sed, iaculis mi. Vivamus maximus ac massa at varius. Nullam viverra nibh sed pharetra aliquet. Mauris id lorem cursus, aliquam quam eu, vehicula magna. Nulla rutrum a sem sed tincidunt. Aliquam id ligula ac ex pharetra commodo ut eget augue. Aenean vehicula vitae velit rutrum vehicula.',
  //   image: 'about3.jpg'
  // },
  // {
  //   title: 'Personal',
  //   content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam vulputate tellus ac auctor fringilla. Integer convallis sem quis magna rutrum vehicula. Donec volutpat, quam non facilisis tempus, neque leo sollicitudin dui, quis sollicitudin risus nibh at turpis.',
  //   image: 'about4.jpg'
  // },
  // {
  //   title: 'Nature',
  //   content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam vulputate tellus ac auctor fringilla. Integer convallis sem quis magna rutrum vehicula. Donec volutpat, quam non facilisis tempus, neque leo sollicitudin dui, quis sollicitudin risus nibh at turpis. Aenean vel mollis ligula, at commodo felis. Donec convallis ac eros quis feugiat. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum condimentum ex mattis, luctus metus sed, iaculis mi. Vivamus maximus ac massa at varius',
  //   image: 'about5.jpg'
  // }
]

export default {
  name: 'About',
  data () {
    return {
      abouts
    }
  }
}
</script>

<style lang="scss" scoped>
  .my-bg{
    background-color: rgba(255, 255, 255, 0.9);
  }
  .my-title{
    background-color: rgba(0, 0, 0, 0.47);
  }
  img{
    object-fit: cover;
  }
  .shadow{
    display:inline-block;
    position:relative;
  }
  .shadow:before{
    display:block;
    content:'';
    position:absolute;
    width:100%;
    height:100%;
    -moz-box-shadow:inset 0px 0px 8px 4px #fff;
    -webkit-box-shadow:inset 0px 0px 8px 4px #fff;
    box-shadow:inset 0px 0px 8px 4px #fff;
  }
</style>
