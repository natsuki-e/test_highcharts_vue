<template>
  <div>
    <highcharts :options="chartOptions"></highcharts>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Chart } from "highcharts-vue";
import Highcharts from "highcharts";
import loadFunnel from "highcharts/modules/funnel";

if (typeof Highcharts === "object") {
  loadFunnel(Highcharts);
}

export type DataType = {
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
      graph: {
        chart: {
          type: "funnel",
        },
        dataLabels: {
          enabled: true,
          format: "<b>{point.name}</b> ({point.y:,.0f})",
          softConnector: true,
        },
        center: ["50%", "50%"],
        neckWidth: "0%",
        neckHeight: "0%",
        width: "80%",
        tooltip: {
          pointFormat: "{series.name}：{point.y:.1f} ℃",
        },
        legend: {
          enabled: false,
        },
        series: [
          {
            name: "Unique users",
            data: [
              ["Website visits", 15654],
              ["Downloads", 4064],
              ["Requested price list", 1987],
              ["Invoice sent", 976],
              ["Finalized", 846],
            ],
          },
        ],
      },
    };
  }
}
</script>
