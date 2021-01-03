<!--
 * @Descripttion: 
 * @version: 
 * @Author: yanghui
 * @Date: 2020-12-23 13:13:37
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2021-01-03 14:30:29
-->
## 折线图负数在整个图上面
效果图：
![效果图](https://github.com/sunshineyanghui/echarts-zhexiantu-demo/blob/master/images/pic.gif)
> echarts实现波拼图，并可以放大，负数在x轴上方

## 代码事例
```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport"
    content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>波形图</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      background-color: #fff;
    }
  </style>

  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script> 
</head>

<body>

  <div id="main" style="width: 100%;height:503px;overflow: hidden;"></div>

  <script type="text/javascript">
  
    function showLine2(str) {
      console.log(str)
      var edata = JSON.parse(str)
      var myChart = echarts.init(document.getElementById('main'));
      // 图表的配置项和数据
      var option = {
        
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        toolbox: {
          show: false,
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          axisLine: {
            onZero: false,
            color: '#666669',
            lineStyle: {
              type: 'solid',
              color: '#666669',//左边线的颜色
              width:'1'//坐标线的宽度
            }
          },
          name: '秒',
          axisLabel: {
            formatter: '{value} ',
            color: '#666669'
          },
          data: edata.arr1
        },
        yAxis: {
          name: 'mm/s',
          type: 'value',
          axisLabel: {
            formatter: '{value} ',
            color: '#666669'
          },
          splitLine: {
            lineStyle: {
              color: "#EEEEF1"
            }
          },
          axisLine: {
            color: '#666669',
            lineStyle: {
              type: 'solid',
              color: '#666669',//左边线的颜色
              width:'1'//坐标线的宽度
            }
          },
          axisPointer: {
            snap: true
          }
        },
        visualMap: {
          show: false,
          dimension: 0,
          pieces: [{
            lte: 6,
            color: '#FF4A4A'
          }, {
            gt: 6,
            lte: 8,
            color: '#FF4A4A'
          }, {
            gt: 8,
            lte: 14,
            color: '#FF4A4A'
          }, {
            gt: 14,
            lte: 17,
            color: '#FF4A4A'
          }, {
            gt: 17,
            color: '#FF4A4A'
          }]
        },
        dataZoom: [{
          show: true,
          type: 'inside',
          filterMode: 'none',
          // xAxisIndex: [0],
          // startValue: -20,
          // endValue: 20
        }, {
          show: true,
          type: 'inside',
          filterMode: 'none',
          // yAxisIndex: [0],
          // startValue: -20,
          // endValue: 20
        }],
        series: [{
          itemStyle : {
            normal : {
              lineStyle:{
                color:'#FF4A4A'
              }
            }
          },
          name: '秒',
          type: 'line',
          smooth: true,
          data: edata.arr2,
        }]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
      myChart.on('click', function (params) {
        console.log(params)
        let data = {
          x: params.name,
          y: params.value
        }
        console.log(data)
        alert(JSON.stringify(data))
        // window.webkit.messageHandlers.iOSObj.postMessage(data)
      });
    }
    let data = {
      arr1: [
        0.0,4.0E-5,0.00184,0.00188,0.00191,0.00223,0.00371,0.00379,0.00383,0.00492
      ],
      arr2: [
        0.0,-0.3,13.6,11.0,12.5,13.2,2.8,2.8,3.2,-2.6
      ]
    }
    let str = JSON.stringify(data)
    showLine2(str)
  </script>
</body>

</html>
```