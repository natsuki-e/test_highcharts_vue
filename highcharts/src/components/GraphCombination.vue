<template>
  <div>
    <highcharts :options="graphcombination"></highcharts>
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
  graphcombination: any;
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
      graphcombination: {
        chart: {
          width: 500,
          height: 300,
          // type: "ｌine",
        },
        legend: {
          enabled: "false",
        },
        title: {
          text: "負荷テストのためのセミナーに関するキャンペーン",
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
          max: 1000,
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          pointFormat: "{series.name}：{point.y:.1f} 人",
        },
        series: [
          {
            type: "column",
            name: "申し込み者数",
            data: [875, 731, 888, 733, 866, 703, 902, 658],
            pointPadding: 0.3,
            groupPadding: 0,
          },
          {
            type: "spline",
            name: "申し込み者数累計",
            data: [244, 877, 888, 733, 766, 722, 558, 501],
            pointPadding: 0.1,
            groupPadding: 0,
          },
        ],
      },
    };
  }
}
</script>
