<script setup>
import * as Cesium from 'cesium'
import * as echarts from 'echarts'
import { onMounted } from 'vue'
// onMountend init cesium's viewer
onMounted(() => {
  const viewer = new Cesium.Viewer('cesiumContainer', {
    animation: false, // 是否显示动画控件
    homeButton: false, // 是否显示home键
    geocoder: false, // 是否显示地名查找控件
    baseLayerPicker: false, // 是否显示图层选择控件
    timeline: false, // 是否显示时间线控件
    fullscreenButton: false, // 是否全屏显示
    infoBox: false, // 是否显示点击要素之后显示的信息
    sceneModePicker: false, // 是否显示投影方式控件  三维/二维
    navigationInstructionsInitiallyVisible: false,
    navigationHelpButton: false, // 是否显示帮助信息控件
    orderIndependentTranslucency: false,
    shouldAnimate: true,
    scene3DOnly: false, // 每个几何实例将只能以3D渲染以节省GPU内存
    selectionIndicator: false, // 取消点击有绿框
    // imageryProvider: new Cesium.ArcGisMapServerImageryProvider({
    //   url:'http://services.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer',
    // }),
  })
  // 不加载默认bing的卫星图
  // viewer.imageryLayers.get(0).show = false
  //设置版权等信息不显示
  viewer._cesiumWidget._creditContainer.style.display = 'none'
  //根据太阳位置开启照明
  viewer.scene.globe.enableLighting = true
  //设置初始位置
  // this.viewer.camera.setView({
  //   destination: Cesium.Cartesian3.fromDegrees(116.20, 40.55, 3000000)
  // });
  // 去掉背景，使透明
  // viewer.scene.skyBox.destroy()
  // viewer.scene.skyBox = undefined
  // viewer.scene.sun.destroy()
  // viewer.scene.sun = undefined
  // viewer.scene.moon.destroy()
  // viewer.scene.moon = undefined
  // viewer.scene.skyAtmosphere.destroy()
  // viewer.scene.skyAtmosphere = undefined
  // viewer.scene.backgroundColor = new Cesium.Color(0, 0, 0, 0)
  viewer.camera.flyTo({
    destination: Cesium.Cartesian3.fromDegrees(
      106.435314,
      40.960521,
      9000000.0
    ),
    duration: 6,
  })

  // 基于准备好的dom，初始化echarts实例
  let chart1 = echarts.init(document.getElementById('chart1'))
  let chart2 = echarts.init(document.getElementById('chart2'))
  let chart3 = echarts.init(document.getElementById('chart3'))
  let chart4 = echarts.init(document.getElementById('chart4'))
  let chart5 = echarts.init(document.getElementById('chart5'))
  let chart6 = echarts.init(document.getElementById('chart6'))
  // chart1
  chart1.setOption({
    title: {
      text: '图表1',
      left: '30%',
      top: '0',
    },
    tooltip: {},
    xAxis: {
      data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子'],
    },
    yAxis: {},
    series: [
      {
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20, 20, 36, 10, 10, 20],
      },
    ],
  })
  // chart2
  chart2.setOption({
  tooltip: {
    trigger: 'item'
  },
  legend: {
    top: '5%',
    left: 'center'
  },
  series: [
    {
      name: 'Access From',
      type: 'pie',
      radius: ['40%', '70%'],
      avoidLabelOverlap: false,
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: '40',
          fontWeight: 'bold'
        }
      },
      labelLine: {
        show: false
      },
      data: [
        { value: 1048, name: 'Search Engine' },
        { value: 735, name: 'Direct' },
        { value: 580, name: 'Email' },
        { value: 484, name: 'Union Ads' },
        { value: 300, name: 'Video Ads' }
      ]
    }
  ]
})
  // chart3
  chart3.setOption({
    title: {
      text: 'Waterfall Chart',
      subtext: 'Living Expenses in Shenzhen',
    },
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'shadow',
      },
      formatter: function (params) {
        var tar = params[1]
        return tar.name + '<br/>' + tar.seriesName + ' : ' + tar.value
      },
    },
    grid: {
      left: '3%',
      right: '4%',
      bottom: '3%',
      containLabel: true,
    },
    xAxis: {
      type: 'category',
      splitLine: { show: false },
      data: ['Total', 'Rent', 'Utilities', 'Transportation', 'Meals', 'Other'],
    },
    yAxis: {
      type: 'value',
    },
    series: [
      {
        name: 'Placeholder',
        type: 'bar',
        stack: 'Total',
        itemStyle: {
          borderColor: 'transparent',
          color: 'transparent',
        },
        emphasis: {
          itemStyle: {
            borderColor: 'transparent',
            color: 'transparent',
          },
        },
        data: [0, 1700, 1400, 1200, 300, 0],
      },
      {
        name: 'Life Cost',
        type: 'bar',
        stack: 'Total',
        label: {
          show: true,
          position: 'inside',
        },
        data: [2900, 1200, 300, 200, 900, 300],
      },
    ],
  })
  // chart4
  chart4.setOption({
    tooltip: {},
    xAxis: {
      data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子'],
    },
    yAxis: {},
    series: [
      {
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20, 20, 36, 10, 10, 20],
      },
    ],
  })
  // chart5
  chart5.setOption({
    title: {
      text: 'Temperature Change in the Coming Week',
    },
    tooltip: {
      trigger: 'axis',
    },
    legend: {},
    toolbox: {
      show: true,
      feature: {
        dataZoom: {
          yAxisIndex: 'none',
        },
        dataView: { readOnly: false },
        magicType: { type: ['line', 'bar'] },
        restore: {},
        saveAsImage: {},
      },
    },
    xAxis: {
      type: 'category',
      boundaryGap: false,
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    },
    yAxis: {
      type: 'value',
      axisLabel: {
        formatter: '{value} °C',
      },
    },
    series: [
      {
        name: 'Highest',
        type: 'line',
        data: [10, 11, 13, 11, 12, 12, 9],
        markPoint: {
          data: [
            { type: 'max', name: 'Max' },
            { type: 'min', name: 'Min' },
          ],
        },
        markLine: {
          data: [{ type: 'average', name: 'Avg' }],
        },
      },
      {
        name: 'Lowest',
        type: 'line',
        data: [1, -2, 2, 5, 3, 2, 0],
        markPoint: {
          data: [{ name: '周最低', value: -2, xAxis: 1, yAxis: -1.5 }],
        },
        markLine: {
          data: [
            { type: 'average', name: 'Avg' },
            [
              {
                symbol: 'none',
                x: '90%',
                yAxis: 'max',
              },
              {
                symbol: 'circle',
                label: {
                  position: 'start',
                  formatter: 'Max',
                },
                type: 'max',
                name: '最高点',
              },
            ],
          ],
        },
      },
    ],
  })
  // chart6
  chart6.setOption({
    xAxis: {
      type: 'category',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    },
    yAxis: {
      type: 'value',
    },
    series: [
      {
        data: [150, 230, 224, 218, 135, 147, 260],
        type: 'line',
      },
    ],
  })
})
</script>

<template>
  <div id="cesiumContainer">
    <div class="chart">
      <div class="left moveLeft">
        <div id="chart1" class="left-chart moveLeft"></div>
        <div id="chart2" class="left-chart moveLeft"></div>
        <div id="chart3" class="left-chart moveLeft"></div>
      </div>
      <div class="center moveTop">
        <p>技术可行性测试标题</p>
      </div>
      <div class="right moveRight">
        <div id="chart4" class="right-chart moveRight"></div>
        <div id="chart5" class="right-chart moveRight"></div>
        <div id="chart6" class="right-chart moveRight"></div>
      </div>
    </div>
  </div>
</template>

<style>
html,
body,
#app,
#cesiumContainer {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.chart {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 999;
  background: transparent;
}
.left,
.right {
  width: 350px;
  height: 100%;
  background: rgba(255, 255, 255, 0.25);
}
.left {
  position: absolute;
  left: 0;
}
.right {
  position: absolute;
  right: 0;
}
.center {
  position: absolute;
  left: 350px;
  width: calc(100% - 700px);
  height: 80px;
  line-height: 80px;
  background: rgba(255, 255, 255, 0.25);
  color: #fff;
  text-align: center;
  font-size: 30px;
}
.center p {
  padding: 0;
  margin: 0;
}
.left-chart,
.right-chart {
  width: 100%;
  height: 33.3%;
}

@keyframes moveLeft {
   from { 
    transform: translateX(-300px);
    opacity: 0; 
  }
  to { 
    transform: translateX(0px);
    opacity: 1; 
  }
}
@keyframes moveRight {
   from { 
    transform: translateX(300px);
    opacity: 0; 
  }
  to { 
    transform: translateX(0px);
    opacity: 1; 
  }
}
@keyframes moveTop {
   from { 
    transform: translateY(-100px);
    opacity: 0; 
  }
  to { 
    transform: translateY(0px);
    opacity: 1; 
  }
}
.moveLeft{
  animation: moveLeft 1s ease-in-out;
}
.moveRight{
  animation: moveRight 1s ease-in-out;
}
.moveTop{
  animation:moveTop 1s ease-in-out
}
</style>
