---
title: echarts柱状图实用配置
date: 2021-09-02
tags: 图表类
categories: 插件
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/15.jpg
summary: 熟练使用echarts的API
top: true
---





## echart柱状图各部分分析

详细配置在最后【图表基本配置项和数据】部分

![image.png](https://gitee.com/Olivivian/PicGoImages/raw/master/img//https/p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2021/09/02/680a9e3ebf954790aa16b6e0bdafaf75-tplv-k3u1fbpfcp-watermark.png)



## echarts设置柱状图【粗细大小】

主要属性`series > barWidth：`

```
barWidth: 20  //设置柱状图大小
```



## echarts设置柱状图【颜色渐变】

主要属性`series > itemStyle > normal > color：`

```
series: [{
      //设置柱状图渐变颜色
      itemStyle: {
        normal: {
          color: new echarts.graphic.LinearGradient(0, 1, 0, 0, [{
            offset: 0,
            color: "#1268f3" // 0% 处的颜色
          }, {
            offset: 0.6,
            color: "#08a4fa" // 60% 处的颜色
          }, {
            offset: 1,
            color: "#01ccfe" // 100% 处的颜色
          }], false)
        }
      },
    }]
```



## echarts 设置柱状图 【柱顶部显示数字】

主要属性`series > itemStyle > normal > label：`

```
series: [{
      itemStyle: {
        normal: {
          label: {
            show: true,     //开启显示
            position: 'top',    //在上方显示
            textStyle: {        //数值样式
              color: 'black',
              fontSize: 16
            }
          }
        }
      },
    }]
```



## echarts 柱状图设置【不同的颜色】，并且自动循环已有颜色；


![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/77e92dccfd07461992ff7fcdb60522e8~tplv-k3u1fbpfcp-watermark.image)

主要属性`series > itemStyle > normal > label`：

按数组顺序显示颜色，如果柱体数量大于颜色数量，则循环已有颜色
```
itemStyle: {
        normal: {
          //这里是重点
          color: function(params) {
            var colorList = ['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83', '#ca8622'];
            // var colorList = ['#c23531','#2f4554', '#61a0a8'];
            // 自动循环已经有的颜色
            return colorList[params.dataIndex % colorList.length];
          }
        }
      }
```



## echart图表基本配置项和数据

### 标题title
```
 title: {
        text: '柱状图示例',                
        textStyle:{	//---主标题内容样式	
            color:'#000',
        },
        subtext:'作者：Axjy',
        subtextStyle:{//---副标题内容样式
            color:'#bbb'            	
        },
        padding:[10,0,0,0]//---标题位置,因为图形是是放在一个dom中,因此用padding属性来定位
    },
```

### 图例legend
```
 legend: {
      type:'plain',//----图例类型，默认为'plain'，当图例很多时可使用'scroll'
      top:'1%',//----图例相对容器位置,top\bottom\left\right
      textStyle:{					//----图例内容样式
        color:'#000',				//---所有图例的字体颜色
        //backgroundColor:'black',	//---所有图例的字体背景色
       },    
      data: [//----图例内容					
        {
            name:'销量',
            icon:'roundRect',//----图例的外框样式'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow', 'none'
            textStyle:{
                color:'#000',		//----单独设置某一个图例的颜色
                //backgroundColor:'black',//---单独设置某一个图例的字体背景色
            }
        }
      ]
    },
```
### grid区域
```
 grid:{
        show:false,					//---是否显示直角坐标系网格
        top:80,						//---相对位置，top\bottom\left\right  
        tooltip:{					//---鼠标焦点放在图形上，产生的提示框
            show:true,	
            trigger:'item',			//---触发类型
            textStyle:{  //---提示框样式
                color:'#fff',
            },
        }
    },
```
### x轴和y轴属性基本相同
```
 xAxis(yAxis): {
        show:true,			//---是否显示
        name:'月份',      //---轴名称
        position:'bottom',	//---x轴位置'top','bottom'
        offset:15,		//---x轴相对于默认位置的偏移
        nameLocation:'start',	//---轴名称相对位置'start','center','end'
        nameTextStyle:{	//---坐标轴名称样式
            color:"#000",
            padding:[5,0,0,-5],	//---坐标轴名称相对位置
        },
        nameGap:15,					//---坐标轴名称与轴线之间的距离
        nameRotate:0,			//---坐标轴名字旋转
        data: ['1月', '2月', '3月', '4月', '5月','6月', '7月'],
    },
```
### 坐标轴  轴线
`xAxis>axisLine 或 yAxis>axisLine`
```
 axisLine:{//---坐标轴 轴线
            show:true,	//---是否显示 
            //------------------- 箭头 -------------------------
            symbol:['none', 'arrow'],	//---是否显示轴线箭头
            symbolSize:[8, 8] ,//---箭头大小
            symbolOffset:[0,7],	//---箭头位置
            
            //------------------- 线 -------------------------
            lineStyle:{
                color:'#000',
                width:1,
                type:'solid',
            },
        },
```
### 坐标轴 刻度
`xAxis>axisTick 或 yAxis>axisTick`
```
  axisTick:{//---坐标轴 刻度
        show:true,//---是否显示
        inside:false,//---是否朝内
        lengt:3,//---长度
        lineStyle:{
            //color:'red',//---默认取轴线的颜色
            width:1,
            type:'solid',
        },
    },
```

### 坐标轴 标签
`xAxis>axisLabel 或 yAxis>axisLabel`
```
 axisLabel:{//---坐标轴 标签
        show:true,//---是否显示
        inside:false,//---是否朝内
        rotate:10,//---旋转角度	
        margin: 8,//---刻度标签与轴线之间的距离
        //color:'red',	//---默认取轴线的颜色
},
```
### grid 区域中的分隔线
`xAxis>splitLine 或 yAxis>splitLine`
```
splitLine:{//---grid 区域中的分隔线(一般y轴的显示，x轴的不显示)
        show:false,//---是否显示，'category'类目轴不显示，此时我的y轴为类目轴，splitLine属性是有意义的
        lineStyle:{
            color:'#666',
            width:1,
            type:'dashed',//---类型'solid'，'dashed'，'dotted'
        },
    },
```
