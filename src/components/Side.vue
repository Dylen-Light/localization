<template>
    <v-navigation-drawer>
        <v-list>
            <v-list-item title="Accessible APs"></v-list-item>
            <v-expansion-panels v-model="panel" multiple  variant="popout">
                <v-expansion-panel v-for="info in AP_info" >
                    <v-expansion-panel-title>
                        AP : {{ info.apid }}
                    </v-expansion-panel-title>
                    <v-expansion-panel-text>
                        <v-card :subtitle=info.isValid>

                            <v-card-title>
                                Position:[{{ info.pos_x }},{{ info.pos_y }}]
                            </v-card-title>

                            <v-card-subtitle>
                                isValid:{{ info.isValid }}
                            </v-card-subtitle>
                            <v-card-text>
                                current distance: {{ info.distance }}
                                <br>isLoS: {{info.isLoS }}
                            </v-card-text>
                        </v-card>
                    </v-expansion-panel-text>
                </v-expansion-panel>
            </v-expansion-panels>
        </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
    created() {
        
    },
    data() {
        return {
            panel: [],
            AP_info: [
                {
                    apid:0,
                    pos_x:0,
                    pos_y:0,
                    isValid: true,
                    distance: 0,
                    isLoS: true
                }, {
                    apid:1,
                    pos_x:1,
                    pos_y:1,
                    isValid: false,
                    distance: 0,
                    isLoS: false
                }
            ]
        }
    },
}

// const AP_info = reactive([{
//     bssid: "ftm_00000000",
//     isValid: true,
//     distance: 0,
//     isLoS: true
// }],
//     [{
//         bssid: "ftm_00000001",
//         isValid: false,
//         distance: 0,
//         isLoS: false
//     }]);
// export default{
//   name:"Index",
//   data() {
//     return {
//         AP_info: [{
//                 apid:-1,
//                 bssid: "ftm_00000000",
//                 isValid: true,
//                 distance: 0,
//                 isLoS: true
//             }]

//         }
//   },
//   created(){
//   },
//   methods:{
//     // login(){
//     //   const _this = this;
//     //   _this.$router.push("/login");
//     // }
//   }
// }


</script>