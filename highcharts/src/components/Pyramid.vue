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
  chartOptions: any;
};

@Component({
  components: {
    highcharts: Chart,
  },
})
export default class Graph extends Vue {
  data(): DataType {
    return {
      chartOptions: {
        chart: {
          type: "funnel",
          width: 500,
          height: 300,
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
          pointFormat:
            "{series.name}: {point.percentage:.1f} % <br>{point.y:,.0f}",
        },
        legend: {
          enabled: false,
        },
        series: [
          {
            name: "Unique users",
            data: [
              ["申し込み者数", 42],
              ["参加者数", 0],
              ["アンケート数", 0],
            ],
          },
        ],
        responsive: {
          rules: [
            {
              condition: {
                maxWidth: 500,
              },
              chartOptions: {
                plotOptions: {
                  series: {
                    dataLabels: {
                      format:
                        "<b>{point.name}</b><br> {point.percentage:.1f} %({point.y})",
                      softConnector: true,
                      borderRadius: 5,
                      borderWidth: 1,
                      borderColor: "#AAA",
                    },
                    center: ["50%", "50%"],
                    width: "50%",
                    neckHeight: "0",
                    neckWidth: "0",
                  },
                },
              },
            },
          ],
        },
      },
    };
  }
}
</script>
