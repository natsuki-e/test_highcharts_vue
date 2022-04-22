<template>
  <div>
    <highcharts :options="tripleBar"></highcharts>
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
  tripleBar: any;
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
      tripleBar: {
        chart: {
          width: 500,
          height: 300,
          type: "column",
        },
        legend: {
          enabled: "true",
        },
        title: {
          text: "",
        },
        subtitle: {
          text: "",
        },
        xAxis: {
          categories: [
            "負荷テストのためのセミナー関・・・",
            "オンラインセミナー第一弾",
            "まだ間に合う！売上・予約デ・・・",
            "キャンペーンA",
            "キャンペーンB",
            "キャンペーンC",
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
            data: [880, 489, 611, 771, 780, 512],
            pointPadding: 0.2,
            groupPadding: 0.1,
          },
          {
            type: "column",
            name: "参加者数",
            data: [811, 489, 233, 602, 633, 342],
            pointPadding: 0.2,
            groupPadding: 0.1,
          },
          {
            type: "column",
            name: "アンケート数",
            data: [750, 200, 478, 498, 489, 512],
            pointPadding: 0.2,
            groupPadding: 0.1,
          },
        ],
      },
    };
  }
}
</script>
