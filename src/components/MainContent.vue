<template>
    <v-navigation-drawer style="width: 20%;">
        <v-list>
            <v-list-item title="Accessible APs"></v-list-item>
            <v-expansion-panels v-model="panel" multiple variant="popout">
                <v-expansion-panel v-for="info in AP_info">
                    <v-expansion-panel-title>
                        AP : {{ info.apid }}
                    </v-expansion-panel-title>
                    <v-expansion-panel-text>
                        <v-card>
                            <v-card-title>
                                Position:[{{ info.pos_x }},{{ info.pos_y }}]
                            </v-card-title>
                            <v-card-text>
                                current distance: {{ info.dist }}
                                <br>isLoS: {{ info.isLoS }}
                                <br>isValid:{{ info.isValid }}
                            </v-card-text>
                        </v-card>
                    </v-expansion-panel-text>
                </v-expansion-panel>
            </v-expansion-panels>
        </v-list>
    </v-navigation-drawer>
    <v-main class="d-flex align-center justify-center" style="min-height: 300px;height: 100%;">
        <div ref="myChart" id="myChart" style="height: 100%; width: 100%;">
        </div>
    </v-main>
</template>

<script>
import axios from 'axios';
import * as echarts from 'echarts';

export default {
    created() {

    },
    mounted() {
        setInterval(() => {
            const dom = this.$refs['myChart']; // 获取dom节点
            const myChart = echarts.init(dom); // 初始化echarts实例
            // 设置实例参数
            myChart.setOption(this.option);
            const _this = this;
            _this.AP_info = [];
            _this.option.series = [];
            axios.get('http://localhost:5000/ap')
                .then(response => {

                    for (let i = 0; i < response.data.length; i++) {
                        let current_data = response.data[i];
                        console.log(current_data);
                        _this.AP_info.push(
                            {
                                apid: current_data.apid,
                                pos_x: current_data.pos_x,
                                pos_y: current_data.pos_y,
                                isValid: Boolean(current_data.is_valid),
                                dist: current_data.dist.toFixed(2) + " cm",
                                isLoS: Boolean(current_data.is_los),
                            }
                        );
                        _this.option.series.push(
                            {
                                type: 'scatter',
                                symbolSize: current_data.dist*2,
                                data: [
                                    [current_data.pos_x, current_data.pos_y]
                                ]
                            },
                            {
                                type: 'effectScatter',
                                symbolSize: 20,
                                data: [
                                    [current_data.pos_x, current_data.pos_y]
                                ]
                            }
                        )
                    }
                    //console.log(_this.AP_info);

                })
                .catch(error => {
                    console.log(error);
                });

            axios.get('http://localhost:5000/res')
                .then(response => {
                    console.log(response.data);
                    _this.option.series.push(
                        {
                            type: 'scatter',
                            symbolSize: 20,
                            data: [
                                [response.data[0], response.data[1]]
                            ]
                        }
                    )

                })
                .catch(error => {
                    console.log(error);
                })
            
        }, 1000 * 5);
    },
    data() {
        return {
            panel: [],
            AP_info: [],
            option: {
                xAxis: {
                    scale: true
                },
                yAxis: {
                    scale: true
                },
                series: [
                    // {
                    //     type: 'scatter',
                    //     symbolSize: 200,
                    //     data: [
                    //         [172.7, 115.2],
                    //         [163.4, 42]
                    //     ]
                    // },
                    // {
                    //     type: 'effectScatter',
                    //     symbolSize: 20,
                    //     data: [
                    //         [172.7, 115.2],
                    //         [163.4, 42]
                    //     ]
                    // },
                ]
            }
        }
    },
    methods: {

    },
}



</script>