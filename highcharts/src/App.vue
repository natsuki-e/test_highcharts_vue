<template>
  <div id="app">
    <v-card>
      <div id="main">
        <div><b>登録会員数</b></div>
        <div>{{ title }}人</div>
      </div>
      <div id="sub">
        <div class="flex-item subtitle">前の期間: {{ subtitle }}%</div>
        <div v-if="subtitle > 100" class="flex-item subtitle" id="uparrow">
          ➚
        </div>
        <div v-else class="flex-item" id="downarrow">➘</div>
        <div class="flex-item subtitle">前年比: {{ subYeartitle }}%</div>
        <div v-if="subYeartitle > 100" class="flex-item subtitle" id="uparrow">
          ➚
        </div>
        <div v-else class="flex-item" id="downarrow">➘</div>
      </div>
      <Graph></Graph>
    </v-card>
    <v-card>
      <div id="main">
        <div><b>PV数</b></div>
        <div>{{ pageview }}</div>
      </div>
      <div id="sub">
        <div class="flex-item subtitle">前の期間: {{ subpageview }}%</div>
        <div v-if="subpageview > 100" class="flex-item subtitle" id="uparrow">
          ➚
        </div>
        <div v-else class="flex-item" id="downarrow">➘</div>
        <div class="flex-item subtitle">前年比: {{ subYearpageview }}%</div>
        <div
          v-if="subYearpageview > 100"
          class="flex-item subtitle"
          id="uparrow"
        >
          ➚
        </div>
        <div v-else class="flex-item" id="downarrow">➘</div>
      </div>
      <GraphBar></GraphBar>
    </v-card>
    <!-- <div>
      <video-player :options="videoOptions" />
    </div> -->
    <v-card>
      <pre>{{ currentTime }}</pre>
      <video
        ref="sampleVid"
        id="sampleVid"
        controls
        @timeupdate="currentTime_ = $event.target.currentTime"
      >
        <source src="./camping.mp4" type="video/mp4" />
      </video>
      <GraphVideo></GraphVideo>
    </v-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Graph from "@/components/Graph.vue";
import GraphBar from "@/components/GraphBar.vue";
import GraphVideo from "@/components/GraphVideo.vue";
// import VideoPlayer from "@/components/VideoPlayer.vue";
import "video.js/dist/video-js.css";

@Component({
  components: {
    Graph,
    GraphBar,
    GraphVideo,
    // VideoPlayer,
  },
})
export default class App extends Vue {
  title = 8000;
  beforesum = 6800;
  beforeYearsum = 3200;
  pageview = 1200;
  beforepageview = 600;
  beforeYearpageview = 300;
  subtitle = Math.round((this.title / this.beforesum) * 100);
  subYeartitle = Math.round((this.title / this.beforeYearsum) * 100);
  subpageview = Math.round((this.pageview / this.beforepageview) * 100);
  subYearpageview = Math.round((this.pageview / this.beforeYearpageview) * 100);
  currentTime_ = 0;
  private get currentTime(): number {
    return this.currentTime_;
  }
  private set currentTime(time) {
    // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    // @ts-ignore
    this.$refs.sampleVid.currentTime = time;
  }
  // videoOptions!: {
  //   autoplay = true;
  //   controls = true;
  //   sources: [
  //     {
  //       src: "./videos/camping_-_111763 (Original).mp4";
  //       type: "video/mp4";
  //     }
  //   ];
  // };
}
</script>

<style>
#main {
  display: flex;
  font-size: 2em;
}
#main > div:last-of-type {
  margin-left: 200px;
}
#sub {
  display: flex;
  font-size: 1.5em;
  text-align: left;
  display: -webkit-box;
  display: -ms-flexbox;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
}
#uparrow {
  font-size: 2em;
  color: red;
}
#downarrow {
  font-size: 2em;
}
/* .flex-item {
  flex-basis: 100%;
} */
.subtitle {
  text-align: center;
  display: -webkit-box;
  display: -ms-flexbox;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
}
#sampleVid {
  width: 500px;
  height: 300;
}
</style>
