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
                    legend: {},
                    tooltip: {},
                    dataset: {
                        dimensions: ['product', '2015', '2016', '2017'],
                        source: [
                            { product: 'Matcha Latte', 2015: 43.3, 2016: 85.8, 2017: 93.7 },
                            { product: 'Milk Tea', 2015: 83.1, 2016: 73.4, 2017: 55.1 },
                            { product: 'Cheese Cocoa', 2015: 86.4, 2016: 65.2, 2017: 82.5 },
                            { product: 'Walnut Brownie', 2015: 72.4, 2016: 53.9, 2017: 39.1 }
                        ]
                    },
                    xAxis: { type: 'category' },
                    yAxis: {},
                    // Declare several bar series, each will be mapped
                    // to a column of dataset.source by default.
                    series: [{ type: 'bar' }, { type: 'bar' }, { type: 'bar' }]
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