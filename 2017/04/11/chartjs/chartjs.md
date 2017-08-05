---
title: chart.js上手
date: 2017-04-11 23:39:14
tags: js
---

### 最近在练习Django，碰到一些数据想通过表格呈现出来，找到了chart.js

```javascript
<canvas id="myChart" width="400" height="400"></canvas>
<script>
var ctx = document.getElementById("myChart");
var myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
        datasets: [{
            label: '# of Votes',
            data: [12, 19, 3, 5, 2, 3],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255,99,132,1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero:true
                }
            }]
        }
    }
});
</script>
```
* [官方文档]:http://www.chartjs.org/docs/ 的示例代码复制进来
* 坑1 : 直接用是图标大小是100% , 应在canvas外包一个div通过css控制 , 再在option加上
```javascript
responsive: true,
maintainAspectRatio: false,
```
* 参考 https://github.com/chartjs/Chart.js/issues/2958
* 通过django传送数据js接受很方便
* chartjs的样式还有一些属性都很炫酷 等待发掘