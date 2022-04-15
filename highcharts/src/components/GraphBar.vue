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
        xAxis: {
          categories: [
            "1/1",
            "1/2",
            "1/3",
            "1/4",
            "1/5",
            "1/6",
            "1/7",
            "1/8",
            "1/9",
            "1/10",
            "1/11",
            "1/12",
          ],
        },
        yAxis: {
          title: false,
          labels: {
            format: "{value} ",
          },
          opposite: false,
          max: 2000,
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          pointFormat: "{series.name}：{point.y:.1f} ℃",
        },
        plotOptions: {
          series: {
            label: {
              connectorAllowed: false,
            },
            pointStart: 1,
          },
        },
        series: [
          {
            // type: "column",
            data: [500, 1510, 1012, 1441, 1223, 1610, 1734, 1443, 1788, 889],
            pointPadding: 0.1,
            groupPadding: 0,
          },
          {
            // type: "column",
            data: [270, 1664, 1830, 1922, 1678, 1860, 1933, 1622, 1441, 1430],
            pointPadding: 0.1,
            groupPadding: 0,
          },
        ],
      },
    };
  }
}
</script>
