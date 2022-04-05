<template>
  <!-- <div> -->
  <highcharts :options="graphVideo"></highcharts>
  <!-- </div> -->
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Chart } from "highcharts-vue";

export type DataType = {
  sum: number;
  beforesum: number;
  beforeYearsum: number;
  graphVideo: any;
};

// const myvid = $refs.sampleVid;

@Component({
  components: {
    highcharts: Chart,
  },
})
export default class Graph extends Vue {
  //   created(this: any) {
  //     this.sampleVid.addEventListener("timeupdate", function() {
  //     var percent = (this.currentTime / this.duration);
  //     var posicao = (percent * curves.series[0].data.length).toFixed(0);
  //     curves.series[0].data[posicao].select(true);
  // }, false);
  //   }
  data(): DataType {
    return {
      sum: 8000,
      beforesum: 6800,
      beforeYearsum: 3200,
      graphVideo: {
        chart: {
          type: "spline",
          width: 500,
          height: 300,
          margin: [50, 150, 60, 80],
          marginRight: 20,
          marginLeft: 60,
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
          lineWidth: 0,
          minorGridLineWidth: 0,
          lineColor: "transparent",
          minorTickLength: 0,
          tickLength: 0,
          max: 60,
          title: {
            text: "時間",
          },
        },
        yAxis: {
          title: {
            text: "継続率",
          },
          labels: {
            format: "{value} ",
          },
          opposite: false,
          max: 100,
          min: 0,
          plotLines: [
            {
              value: 70.345255,
              color: "#62acdf",
              dashStyle: "dot",
              width: 1,
            },
            {
              value: 29.654745,
              color: "#62acdf",
              dashStyle: "dot",
              width: 1,
            },
          ],
          plotBands: [
            {
              from: 29.654745,
              to: 70.345255,
              color: "rgba(98,172,223,0.1)",
            },
          ],
        },
        credits: {
          enabled: false,
        },
        tooltip: {
          formatter: function (this: any, err: any) {
            return (
              this.x +
              "s<br>" +
              '<span style="color:' +
              this.series.color +
              '">● </span> ' +
              this.series.name +
              ": <b> " +
              this.y?.toFixed(2) +
              "</b>"
            );
          },
          // pointFormat: "{series.name}：{point.y:.1f} %",
          crosshairs: {
            width: 2,
            color: "gray",
            dashStyle: "shortdot",
          },
        },
        series: [
          {
            // type: "column",
            data: [
              100, 92, 95, 90, 85, 89, 83, 79, 82, 81, 80, 80, 77, 76, 75, 74,
              72, 66, 71, 64, 62, 51, 59, 55, 58, 53, 49, 44, 48, 40, 46, 43,
              31, 42, 38, 36, 35, 33, 31, 30, 29, 33, 28, 27, 24, 22, 21, 19,
              18, 11, 9, 8, 8, 6, 12, 14, 16, 11, 8, 5,
            ],
            pointPadding: 0.1,
            groupPadding: 0,
          },
        ],
        plotOptions: {
          allowPointSelect: true,
          series: {
            marker: {
              enabled: false,
            },
          },
          point: {
            events: {
              click: function (this: any) {
                this.sampleVid.currentTime = this.x;
                this.sampleVid.pause();
              },
            },
          },
          marker: {
            radius: 1,
            states: {
              select: {
                radius: 3,
                fillColor: "#62acdf",
                lineColor: "#62acdf",
                lineWidth: 4,
              },
            },
          },
        },
      },
    };
  }
}
</script>
