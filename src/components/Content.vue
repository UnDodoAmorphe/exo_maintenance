<template>
    <v-container>
        <v-row justify="center">
            <v-col md="auto">
                <h1>Hello world</h1>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="6">
                <v-text-field v-model="price" type="number" outlined label="Prix unitaire"></v-text-field>
            </v-col>
            <v-col cols="4">
                <p class="pt-3">{{price}} $</p>
            </v-col>
            <v-spacer></v-spacer>
            <v-col cols="2">
                <v-dialog v-model="dialog" max-width="400">
                    <template v-slot:activator="{ on }">
                        <v-btn color="dark" dark v-on="on">Open help</v-btn>
                    </template>
                    <v-card>
                        <v-card-title class="headline">Infos</v-card-title>
                        <v-card-text>
                            <v-simple-table height="300px">
                                <template v-slot:default>
                                    <thead>
                                        <tr>
                                            <th class="text-left">State</th>
                                            <th class="text-left">Taxe</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr v-for="item in taxeArray" :key="item.id">
                                            <td>{{ item.name }}</td>
                                            <td>{{ item.taxe }}</td>
                                        </tr>
                                    </tbody>
                                </template>
                            </v-simple-table>
                        </v-card-text>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="green darken-1" text @click="dialog = false">Ok</v-btn>
                        </v-card-actions>
                    </v-card>
                </v-dialog>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="6">
                <v-text-field v-model="number" type="number" outlined label="Nombre d'items"></v-text-field>
            </v-col>
            <v-col cols="4">
                <p class="pt-3">{{number}}</p>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="6">
                <v-select :items="taxeArray" label="State" item-text="name" item-value="taxe" v-model="selected"></v-select>
            </v-col>
        </v-row>
        <v-row justify="center">
            <v-col md=auto>
                <p class="pt-3">Order Value : {{orderValue}} $</p>
            </v-col>
        </v-row>
        <v-row justify="center">
            <v-col md=auto>
                <p class="pt-3">NetPrice : {{netPrice}} $</p>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    export default {
        data() {
            return {
                price: null,
                number: null,
                dialog: false,
                taxeArray: [{
                        name: "UT",
                        taxe: 6.85
                    },
                    {
                        name: "NV",
                        taxe: 8.0
                    },
                    {
                        name: "TX",
                        taxe: 6.25
                    },
                    {
                        name: "AL",
                        taxe: 4.0
                    },
                    {
                        name: "CA",
                        taxe: 8.25
                    }

                ],
                selected: null
            }
        },
        computed: {
            orderValue: function() {
                return this.price * this.number
            },
            netPrice: function() {
                let reduc = 0
                if (this.orderValue >= 50000)
                    reduc = 15
                else if (this.orderValue >= 10000)
                    reduc = 10
                else if (this.orderValue >= 7000)
                    reduc = 7
                else if (this.orderValue >= 5000)
                    reduc = 5
                else if (this.orderValue >= 1000)
                    reduc = 3
                return this.orderValue + ((this.orderValue * this.selected / 100) * ((100 - reduc) / 100))
            }
        },
        components: {}
    }

</script>

<style>

</style>
