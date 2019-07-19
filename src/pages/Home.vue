<template>
  <div class="home">
    <div class="home-body">
      <div class="home-header">
        <div class="home-header-left">
          <a class="platform-name">山东省公安交通管理大数据平台</a>
          <span class="current-time">{{current_time}}</span>
        </div>
        <div class="home-header-right">
          <span class="user-info">欢迎您{{username}}</span>
          <a class="exit">退出</a>
        </div>
      </div>
      <div class="home-content">
        <div class="home-info-left">
          <div class="abnormal-info">
            <div class="bg">
              <p>查处违法数量</p>
              <h2 class="red">{{abnormal_num.illegal}}</h2>
              <a class="abnormal-info-detail">查处违法详情></a>
            </div>
            <div class="bg">
              <p>受理事故数量</p>
              <h2 class="red">{{abnormal_num.accident}}</h2>
              <a class="abnormal-info-detail">受理事故详情></a>
            </div>
          </div>
          <h3 class="red title">城市交通信息</h3>
          <div class="car-total bg">
            <div class="car-total-name">
              <span class="white">省际卡口车流量</span>
              <a>详情></a>
            </div>
            <div class="car-total-num">
              <h4 class="red">进省车辆{{car_in_num}}</h4>
              <h4 class="red">出省车辆{{car_out_num}}</h4>
            </div>
          </div>
          <div class="car-total-detail bg">
            <div>
              <span class="white">省际卡口车流量详情</span>
              <a>详情></a>
            </div>
            <ul>
              <li v-for="item in car_detail">
                <span>{{item.k_name}}进省车辆&nbsp;&nbsp;{{item.in_num}}</span>
                <span>出省车辆&nbsp;&nbsp;{{item.out_num}}</span>
              </li>
            </ul>
          </div>
          <div class="car-hs-detail bg">
            <div>
              <span class="white">高速路段详情</span>
              <a>详情></a>
            </div>
            <ul>
              <li v-for="item in highSpeed_detail">
                <span>{{item.name}}</span>
                <span>{{item.num}}</span>
              </li>
            </ul>
          </div>
          <div class="car-hs-toll bg">
            <div>
              <span class="white">高速收费站封闭</span>
              <a>详情></a>
            </div>
            <ul>
              <li v-for="item in highSpeed_toll">
                <span>{{item.name}}</span>
                <span>{{item.state}}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="home-map">
          <img src="../assets/images/map.png">
<!--          <div id="mapChart" :style="{width: '300px', height: '300px'}"></div>-->
          <ul>
            <li>城市概况</li>
            <li>执法系统</li>
            <li>业务系统</li>
            <li>社会服务</li>
          </ul>
        </div>
        <div class="home-info-right">
          <h3 class="red title safeh3">城市安全指数</h3>
          <div class="city_safe_rate">
            <div id="radarChart" :style="{width: '300px', height: '300px'}"></div>
          </div>
          <div class="road-info">
            <div>
              <span class="white">路段信息</span>
              <span class="white">当前选择：<span class="blue">{{road_info.choose}}</span></span>
            </div>
            <ul>
              <li v-for="item in road_info.content">
                <span v-if="item.type" class="red">{{item.time}}{{item.desc}}</span>
                <span v-else>{{item.time}}{{item.desc}}</span>
              </li>
            </ul>
          </div>
          <h3 class="red title">实况路段</h3>
          <div class="car-real-situation">
            <div>
              <span class="white">摄像头数据</span>
              <span>摄像头：{{camera_info.total_num}}</span>
              <span>故障数：{{camera_info.abnormal_num}}</span>
            </div>
            <ul>
              <li v-for="item in camera_info.space">
                <img src="../assets/images/camera_data.jpg">
                <span>{{item.name}}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import $ from 'jquery';
  export default {
    name: "home",
    data() {
      return {
        username: 'jack',
        current_time: '',
        abnormal_num: {
          illegal: 8445,
          accident: 745
        },
        car_in_num: 4586,
        car_out_num: 58766,
        car_detail: [
          {
            k_name: '东郊卡口',
            in_num: 8981,
            out_num: 695
          },
          {
            k_name: '西郊卡口',
            in_num: 232,
            out_num: 321
          },
          {
            k_name: '南郊卡口',
            in_num: 931,
            out_num: 909
          },
          {
            k_name: '北郊卡口',
            in_num: 298,
            out_num: 311
          }
        ],
        highSpeed_detail: [
          {
            name: 'G25 长深高速临沂段 1539KM',
            num: 3231
          },
          {
            name: 'G22 青兰高速黄岛段 73KM',
            num: 1890
          },
          {
            name: 'G35 济广高速菏泽段 251KM',
            num: 2861
          }
        ],
        highSpeed_toll: [
          {
            name: 'G18 荣乌灰壕收费站',
            state: '更换地磅'
          },
          {
            name: 'G22 张家岐收费站',
            state: '临时封闭'
          },
          {
            name: 'G35 河东收费站',
            state: '临时封闭'
          }
        ],
        road_info: {
          choose: '知春路',
          content: [
            {
              time: '08:24',
              desc: '知春路口发生追尾事故',
              type: 1
            },
            {
              time: '09:07',
              desc: '事故处理完毕',
              type: 0
            },
            {
              time: '10:00',
              desc: '交通状况良好',
              type: 0
            },
            {
              time: '12:00',
              desc: '交通状况中',
              type: 0
            },
            {
              time: '12:20',
              desc: '海淀路口发生刮蹭事故',
              type: 1
            },
            {
              time: '12:47',
              desc: '事故处理完毕',
              type: 0
            },
            {
              time: '13:00',
              desc: '交通状况良好',
              type: 0
            },
            {
              time: '13:05',
              desc: '交通状况中',
              type: 0
            },
            {
              time: '13:50',
              desc: '海淀路口发生追尾事故',
              type: 1
            },
            {
              time: '14:17',
              desc: '事故处理完毕',
              type: 0
            }
          ]
        },
        camera_info: {
          total_num: 231,
          abnormal_num: 5,
          space: [
            {
              name: '知春路卡口',
              url: './static/images/camera_data'
            },
            {
              name: '海淀黄庄卡口',
              url: './static/images/camera_data'
            },
            {
              name: '中关村大街卡口',
              url: './static/images/camera_data'
            }
          ]
        }
      }
    },
    methods: {
      // 动态获取当前时间
      getTime() {
        let time = new Date();// 获取当前日期对象
        let year = time.getFullYear();// 获取年份
        let month = time.getMonth() + 1;// 获取月份
        let day = time.getDate();// 获取日
        let hour = time.getHours();// 获取时
        let minute = time.getMinutes();// 获取分
        let second = time.getSeconds();// 获取秒

        this.current_time = year + '.' + month + '.' + day + ' ' + hour + ':' + minute + ':' + second;
        setTimeout(() => {
          this.getTime();
        }, 1000)
      },
      // 绘制雷达图
      drawRadar() {
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('radarChart'))
        // 绘制图表
        myChart.setOption({
          tooltip: {},
          color: ['#88E652', '#1EB1B2'],
          legend: {
            right: 0,
            top: '5px',
            orient: 'vertical',
            data: [
              {
                name: '2017',
                textStyle: {
                  color: 'white'
                }
              },
              {
                name: '2018',
                textStyle: {
                  color: 'white'
                }
              }
            ]
          },
          radar: {
            name: {
              textStyle: {
                color: '#fff',
                borderRadius: 3,
                padding: [3, 5]
              }
            },
            indicator: [
              {name: '设备情况', max: 6500},
              {name: '违章事故', max: 16000},
              {name: '道路情况', max: 30000},
              {name: '地段情况', max: 38000},
              {name: '交通管理', max: 52000},
            ],
            radius: 75
          },
          series: [{
            name: '2017 vs 2018',
            type: 'radar',
            areaStyle: {normal: {}},
            data: [
              {
                value: [4300, 10000, 28000, 35000, 50000],
                name: '2017'
              },
              {
                value: [5000, 14000, 28000, 31000, 42000],
                name: '2018'
              }
            ]
          }]
        });
      },
      // 绘制地图
      drawMap() {
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('mapChart'));
        let app = this;
        let option = null;
        // 绘制图表
        $.get('/static/lines-bus.json', function(data) {
          var hStep = 300 / (data.length - 1);
          var busLines = [].concat.apply([], data.map(function (busLine, idx) {
            var prevPt;
            var points = [];
            for (var i = 0; i < busLine.length; i += 2) {
              var pt = [busLine[i], busLine[i + 1]];
              if (i > 0) {
                pt = [
                  prevPt[0] + pt[0],
                  prevPt[1] + pt[1]
                ];
              }
              prevPt = pt;

              points.push([pt[0] / 1e4, pt[1] / 1e4]);
            }
            return {
              coords: points,
              lineStyle: {
                normal: {
                  color: app.$echarts.color.modifyHSL('#5A94DF', Math.round(hStep * idx))
                }
              }
            };
          }));
          myChart.setOption(option = {
            bmap: {
              center: [116.46, 39.92],
              zoom: 10,
              roam: true,
              mapStyle: {
                'styleJson': [
                  {
                    'featureType': 'water',
                    'elementType': 'all',
                    'stylers': {
                      'color': '#031628'
                    }
                  },
                  {
                    'featureType': 'land',
                    'elementType': 'geometry',
                    'stylers': {
                      'color': '#000102'
                    }
                  },
                  {
                    'featureType': 'highway',
                    'elementType': 'all',
                    'stylers': {
                      'visibility': 'off'
                    }
                  },
                  {
                    'featureType': 'arterial',
                    'elementType': 'geometry.fill',
                    'stylers': {
                      'color': '#000000'
                    }
                  },
                  {
                    'featureType': 'arterial',
                    'elementType': 'geometry.stroke',
                    'stylers': {
                      'color': '#0b3d51'
                    }
                  },
                  {
                    'featureType': 'local',
                    'elementType': 'geometry',
                    'stylers': {
                      'color': '#000000'
                    }
                  },
                  {
                    'featureType': 'railway',
                    'elementType': 'geometry.fill',
                    'stylers': {
                      'color': '#000000'
                    }
                  },
                  {
                    'featureType': 'railway',
                    'elementType': 'geometry.stroke',
                    'stylers': {
                      'color': '#08304b'
                    }
                  },
                  {
                    'featureType': 'subway',
                    'elementType': 'geometry',
                    'stylers': {
                      'lightness': -70
                    }
                  },
                  {
                    'featureType': 'building',
                    'elementType': 'geometry.fill',
                    'stylers': {
                      'color': '#000000'
                    }
                  },
                  {
                    'featureType': 'all',
                    'elementType': 'labels.text.fill',
                    'stylers': {
                      'color': '#857f7f'
                    }
                  },
                  {
                    'featureType': 'all',
                    'elementType': 'labels.text.stroke',
                    'stylers': {
                      'color': '#000000'
                    }
                  },
                  {
                    'featureType': 'building',
                    'elementType': 'geometry',
                    'stylers': {
                      'color': '#022338'
                    }
                  },
                  {
                    'featureType': 'green',
                    'elementType': 'geometry',
                    'stylers': {
                      'color': '#062032'
                    }
                  },
                  {
                    'featureType': 'boundary',
                    'elementType': 'all',
                    'stylers': {
                      'color': '#465b6c'
                    }
                  },
                  {
                    'featureType': 'manmade',
                    'elementType': 'all',
                    'stylers': {
                      'color': '#022338'
                    }
                  },
                  {
                    'featureType': 'label',
                    'elementType': 'all',
                    'stylers': {
                      'visibility': 'off'
                    }
                  }
                ]
              }
            },
            series: [{
              type: 'lines',
              coordinateSystem: 'bmap',
              polyline: true,
              data: busLines,
              silent: true,
              lineStyle: {
                normal: {
                  // color: '#c23531',
                  // color: 'rgb(200, 35, 45)',
                  opacity: 0.2,
                  width: 1
                }
              },
              progressiveThreshold: 500,
              progressive: 200
            }, {
              type: 'lines',
              coordinateSystem: 'bmap',
              polyline: true,
              data: busLines,
              lineStyle: {
                normal: {
                  width: 0
                }
              },
              effect: {
                constantSpeed: 20,
                show: true,
                trailLength: 0.1,
                symbolSize: 1.5
              },
              zlevel: 1
            }]
          });
        });
      }
    },
    mounted() {
      this.getTime();// 获取当前时间
      this.drawRadar();// 绘制雷达图
      // this.drawMap();// 绘制地图
    }
  }
</script>

<style scoped>
  .red {
    color: red;
  }

  .white {
    color: white;
  }

  .blue {
    color: #01C1FD;
  }

  .bg {
    background-color: #1A1A1A;
  }

  .title {
    align-self: flex-start;
    border-left: 4px solid #01C1FD;
    padding-left: 5px;
  }

  .home {
    background-color: black;
  }

  .home-body {
    margin: 0 50px;
  }

  .home-header {
    display: flex;
    justify-content: space-between;
    padding-top: 20px;
  }

  .home-header-left {
    display: flex;
    align-items: center;
    color: white;
  }

  .platform-name {
    background-color: red;
    padding: 20px;
  }

  .current-time {
    margin-left: 20px;
  }

  .home-header-right {
    display: flex;
    align-items: center;
    color: grey;
  }

  .user-info {
    margin-right: 40px;
  }

  .exit {
    margin-right: 20px;
  }

  .home-content {
    display: flex;
    color: grey;
    margin-top: 20px;
  }

  .home-info-left {
    display: flex;
    flex-direction: column;
    flex: 1;
  }

  .abnormal-info {
    display: flex;
    justify-content: space-around;
  }

  .abnormal-info > div {
    padding: 10px;
  }

  .abnormal-info-detail {
    font-size: 12px;
  }

  .car-total-name {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }

  .car-total-num {
    display: flex;
    justify-content: space-around;
  }

  .car-total-detail {
    margin-top: 10px;
  }

  .car-total-detail > div {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }

  .car-total-detail > ul {
    padding: 0;
    margin: 20px 10px;
  }

  .car-total-detail > ul li {
    list-style: none;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
  }

  .car-hs-detail {
    margin-top: 10px;
  }

  .car-hs-detail > div {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }

  .car-hs-detail > ul {
    padding: 0;
    margin: 20px 10px;
  }

  .car-hs-detail > ul li {
    list-style: none;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
  }

  .car-hs-toll {
    margin-top: 10px;
  }

  .car-hs-toll > div {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }

  .car-hs-toll > ul {
    padding: 0;
    margin: 20px 10px;
  }

  .car-hs-toll > ul li {
    list-style: none;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
  }

  .home-map {
    flex: 3;
  }

  .home-map img {
    height: 600px;
  }

  .home-map ul {
    display: flex;
    justify-content: space-around;
  }

  .home-map ul li {
    list-style: none;
    background-color: red;
    color: #ABABAB;
    padding: 5px 10px;
  }

  .home-map ul li:hover {
    color: white;
    border: 2px solid white;
    margin: -2px;
  }

  .home-info-right {
    display: flex;
    flex-direction: column;
    flex: 1;
  }

  .safeh3 {
    margin-top: 0;
  }

  .city_safe_rate {
    background-color: #1A1A1A;
  }

  .city_safe_rate > div {

  }

  .road-info {
    background-color: #1A1A1A;
    margin-top: 10px;
  }

  .road-info > div {
    margin: 10px;
    display: flex;
    justify-content: space-between;
  }

  .road-info > ul {
    padding: 0;
    margin-left: 10px;
    height: 100px;
    overflow: auto;
  }

  .road-info > ul li {
    list-style: none;
    font-size: 12px;
    display: flex;
  }

  .car-real-situation > div {
    display: flex;
    justify-content: space-around;
  }

  .car-real-situation ul {
    padding: 0;
    display: flex;
    justify-content: space-between;
  }

  .car-real-situation ul li {
    list-style: none;
    font-size: 12px;
    display: flex;
    flex-direction: column;
  }

  .car-real-situation ul li img {
    height: 50px;
  }
</style>
