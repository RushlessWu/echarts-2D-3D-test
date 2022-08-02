<template>
  <div>
    <div class="map-container" ref="myEchart"></div>
  </div>
</template>

<script>
/* eslint-disable */
import chinaMapData from "@/china.json";
const echarts = require("echarts");
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      myEchart: null,
      option: {},
    };
  },
  created() {
    this.$nextTick(() => {
      echarts.registerMap("china", chinaMapData);
      let map = echarts.init(this.$refs.myEchart),
        data = [
          // { name: "北京", value: 632, riskNum: 563, riskPointNum: 69 },
          // { name: "黑龙江", value: 1623, riskNum: 948, riskPointNum: 675 },
          // { name: "河北", value: 98, riskNum: 98, riskPointNum: "343" },
        ];

      let options = this.mapChinaOptions(data);

      map.setOption(options);
    });
  },
  methods: {
    /* eslint-disable */

    mapChinaOptions(data, formatter) {
      let max = 0;
      let riskMaxPoint = data.map((item) => {
        return item.riskPointNum;
      });
      if (data && data.length) {
        max = Math.max(...riskMaxPoint);
      }
      return {
        visualMap: {
          show: false,
          min: 0,
          max: max,
        },
        geo: {
          map: "china",
          roam: false, // 一定要关闭拖拽
          zoom: 1.23,
          center: [105, 36], // 调整地图位置
          label: {
            normal: {
              show: false, //关闭省份名展示
              fontSize: "10",
              color: "rgba(0,0,0,0.7)",
            },
            emphasis: {
              show: false,
            },
          },
          itemStyle: {
            normal: {
              areaColor: "#0d0059",
              borderColor: "#389dff",
              borderWidth: 1, //设置外层边框
              shadowBlur: 2,
              shadowOffsetY: 13,
              shadowOffsetX: 15,
              shadowColor: "#1d8fb2",
            },
            emphasis: {
              areaColor: "#184cff",
              shadowOffsetX: 0,
              shadowOffsetY: 0,
              shadowBlur: 5,
              borderWidth: 0,
              shadowColor: "rgba(0, 0, 0, 0.5)",
            },
          },
          regions: [
            {
              name: "南海诸岛",
              itemStyle: {
                normal: {
                  areaColor: "#0d0059",
                  borderColor: "#389dff",
                  borderWidth: 1, //设置外层边框
                  shadowBlur: 2,
                  shadowOffsetY: 0,
                  shadowOffsetX: 0,
                  shadowColor: "#1d8fb2",
                }
              },
            },
          ],
        },

        grid: {
          top: 10,
          bottom: 10,
          width: "1000px",
          height: "500px",
        },
        tooltip: {
          show: false,
          // trigger: "item",
          // formatter: formatter ? formatter : "{b}<br/>{c}",
          // borderColor: "#CB000C",
          // borderWidth: "1",
        },
        dataRange: {
          // 数值范围对应的 取色
          x: "left",
          y: "bottom",
          show: false,
          // splitList: [
          //   { start: 20000, color: "#CB000C" },
          //   { start: 10001, end: 20000, color: "#f1658b" },
          //   { start: 5001, end: 10000, color: "rgba(247,168,190,.8)" },
          //   { end: 5000, color: "#fae8e9" },
          // ],
          // color: ["#fae8e9", "#f7a8be", "#f1658b ", "#CB000C"],
        },
        series: [
          {
            type: "map",
            map: "china",
            roam: false,
            zoom: 1.23,
            center: [105, 36],
            // geoIndex: 1,
            // aspectScale: 0.75, //长宽比
            showLegendSymbol: false,
            itemStyle: {
              normal: {
                areaColor: "#0d0059",
                borderColor: "#389dff",
                borderWidth: 0.5,
              },
              emphasis: {
                areaColor: "#17008d",
                shadowOffsetX: 0,
                shadowOffsetY: 0,
                shadowBlur: 5,
                borderWidth: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)",
              },
            },
            label: {
              fontSize: 12,
              normal: {
                show: true, // 默认 是否显示省份标签
                color: "#fff",
              },
              emphasis: {
                show: true, // 鼠标 hover 时是否显示身份标签
                textStyle: {
                  color: "#fff",
                },
              },
            },
            data: data,
          },
        ],
      };
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map-container {
  height: 100vh;
}
</style>
