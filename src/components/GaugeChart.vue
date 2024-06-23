<template>
    <div ref="chart" class="chart-container"></div>
</template>

<script>
import * as echarts from 'echarts';
import { onMounted, ref } from 'vue';

export default {
    name: 'LineChart',
    setup() {
        const chart = ref(null);
        let myChart = null;

        onMounted(() => {
            const myChart = echarts.init(chart.value);

            const option = {
                xAxis: {
                    type: 'category',
                    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                },
                yAxis: {
                    type: 'value'
                },
                series: [
                    {
                        data: [150, 230, 224, 218, 135, 147, 260],
                        type: 'line'
                    }
                ]
            };

            myChart.setOption(option);
        });


        const initChart = () => {
            if (chart.value) {
                myChart = echarts.init(chart.value);
                const option = {
                    series: [
                        {
                            type: 'gauge',
                            axisLine: {
                                lineStyle: {
                                    width: 30,
                                    color: [
                                        [0.3, '#67e0e3'],
                                        [0.7, '#37a2da'],
                                        [1, '#fd666d']
                                    ]
                                }
                            },
                            pointer: {
                                itemStyle: {
                                    color: 'auto'
                                }
                            },
                            axisTick: {
                                distance: -30,
                                length: 8,
                                lineStyle: {
                                    color: '#fff',
                                    width: 2
                                }
                            },
                            splitLine: {
                                distance: -30,
                                length: 30,
                                lineStyle: {
                                    color: '#fff',
                                    width: 4
                                }
                            },
                            axisLabel: {
                                color: 'inherit',
                                distance: 40,
                                fontSize: 20
                            },
                            detail: {
                                valueAnimation: true,
                                formatter: '{value} km/h',
                                color: 'inherit'
                            },
                            data: [
                                {
                                    value: 70
                                }
                            ]
                        }
                    ]
                };

                myChart.setOption(option);
            }
        };


        const resizeChart = () => {
            if (myChart) {
                myChart.resize();
            }
        };

        onMounted(() => {
            initChart();
            window.addEventListener('resize', resizeChart);
        });


        return {
            chart
        };
    }
};
</script>

<style scoped>
/* 你可以在这里添加一些样式 */
.chart-container {
    width: 100%;
    height: 100%;
    padding: 20px;
}
</style>