<template>
  <div>
    <highcharts :options="graphBar"></highcharts>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Chart } from "highcharts-vue";

export type DataType = {
  sum: number;
  beforesum: number;
  beforeYearsum: number;
  graphBar: any;
};

@Component({
  components: {
    highcharts: Chart,
  },
})
export default class Graph extends Vue {
  data(): DataType {
    return {
      sum: 8000,
      beforesum: 6800,
      beforeYearsum: 3200,
      graphBar: {
        chart: {
          type: "line",
          width: 500,
          height: 300,
        },
        legend: {
          enabled: "false",
        },
        title: {
          text: "",
        },
        subtitle: {
          text: "",
        },
        yAxis: {
          title: false,
          labels: {
            format: "{value} ",
          },
          opposite: false,
          max: 900,
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          pointFormat: "{series.name}：{point.y:.1f} ℃",
        },
        series: [
          {
            // type: "column",
            data: [100, 180, 183, 322, 178, 600, 411, 721, 889],
            pointPadding: 0.1,
            groupPadding: 0,
          },
        ],
      },
    };
  }
}
</script>
