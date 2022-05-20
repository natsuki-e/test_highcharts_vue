<template>
  <div>
    <highcharts :options="graph"></highcharts>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Chart } from "highcharts-vue";
import Highcharts from "highcharts";
import exportingInit from "highcharts/modules/exporting";
import exportingCSV from "highcharts/modules/export-data";

if (typeof Highcharts === "object") {
  exportingInit(Highcharts);
  exportingCSV(Highcharts);
}

export type DataType = {
  sum: number;
  beforesum: number;
  beforeYearsum: number;
  graph: any;
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
      graph: {
        chart: {
          width: 500,
          height: 300,
          type: "ｌine",
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
        xAxis: {
          categories: [
            "1/1",
            "1/7",
            "1/14",
            "1/21",
            "1/28",
            "2/5",
            "2/12",
            "2/19",
            "2/26",
          ],
          crosshair: true,
          categoryPercentage: 0.2,
        },
        yAxis: {
          title: false,
          labels: {
            format: "{value} ",
          },
          opposite: false,
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          pointFormat: "{series.name}：{point.y:.1f} ℃",
        },
        series: [
          {
            type: "column",
            data: [0, 0, 0, 0, 0, 0, 0, 0, 0],
            pointPadding: 0.1,
            groupPadding: 0,
          },
        ],
      },
    };
  }
}
</script>
