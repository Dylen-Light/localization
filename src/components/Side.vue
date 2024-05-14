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
                            <v-card-subtitle>
                                isValid:{{ info.isValid }}
                            </v-card-subtitle>
                            <v-card-text>
                                current distance: {{ info.dist }}
                                <br>isLoS: {{ info.isLoS }}
                            </v-card-text>
                        </v-card>
                    </v-expansion-panel-text>
                </v-expansion-panel>
            </v-expansion-panels>
        </v-list>
    </v-navigation-drawer>
</template>

<script>
import axios from 'axios';

export default {
    created() {
        
    },
    mounted() {
        setInterval(() => {
            axios.get('http://localhost:5000/ap')
                .then(response => {
                    //console.log(response.data);
                    // const array = Object.keys(response.data).map(key => ({
                    //     id: key,
                    //     ...response.data[key]
                    // }));
                    // console.log(array)
                    const _this = this;
                    this.AP_info = [];
                    for (let i = 0; i < response.data.length; i++) {
                        let current_data = response.data[i];
                        console.log(current_data);
                        this.AP_info.push(
                            {
                                apid: current_data.apid,
                                pos_x: current_data.pos_x,
                                pos_y: current_data.pos_y,
                                isValid: Boolean(current_data.is_valid),
                                dist: String(current_data.dist),
                                isLoS: Boolean(current_data.is_los),
                            }
                        )
                    }
                    console.log(_this.AP_info);
                })
                .catch(error => {
                    console.log(error);
                })
        }, 1000 * 5);
    },
    data() {
        return {
            panel: [],
            AP_info: []
        }
    },
    methods: {
        
    },
}



</script>