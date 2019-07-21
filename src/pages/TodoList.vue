<template>
    <div class="list">
      <div class="list-header">
        <label>ToDoList</label>
        <input v-model="taskContent">
        <button @click="submitTask" :disabled="taskContent == ''">提交</button>
      </div>
      <div class="list-content">
        <div class="doing-task">
          <h2>正在进行</h2>
          <ol>
            <li v-for="item in doingTaskList">{{item}}</li>
          </ol>
        </div>
        <div class="done-task">
          <h2>已经完成</h2>
        </div>
      </div>
<!--      <div id="myChart" :style="{width: '300px', height: '300px'}"></div>-->
      <h2>{{msg}}</h2>
      <h2>{{rmsg}}</h2>
      <Row>
        <Col :xs="2" :sm="4" :md="6" :lg="8">Col</Col>
        <Col :xs="20" :sm="16" :md="12" :lg="8">Col</Col>
        <Col :xs="2" :sm="4" :md="6" :lg="8">Col</Col>
      </Row>
    </div>
</template>

<script>
  export default {
    name: "TodoList",
    data(){
      return{
        doingTaskList: [],
        doneTaskList: [],
        taskContent: '',
        msg: 'hello'
      }
    },
    computed:{
      rmsg(){
        return this.msg.split('').reverse().join('');
      }
    },
    mounted(){
      // this.drawLine();// 绘制图表
    },
    methods:{
      submitTask(){
        this.doingTaskList.push(this.taskContent);
        this.taskContent = '';
      },
      // 绘制图表
      drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
          title: { text: '在Vue中使用echarts' },
          tooltip: {},
          xAxis: {
            data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
          },
          yAxis: {},
          series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }]
        });
      }
    }
  }
</script>

<style scoped>
  .list-header{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .list-header input{
    margin: 20px;
  }
</style>
