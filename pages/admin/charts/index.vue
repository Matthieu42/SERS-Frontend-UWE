<template>
    <div id="contenu">

        <div id="form">
        <b-form-select v-model="selected" :options="dropDownOptions" id="formComp"></b-form-select>

        <label v-if="this.selected == 3 || this.selected == 4" id="formComp">Module :</label>
        <b-form-input list="input-list" id="input-with-list" v-if="this.selected == 3 || this.selected == 4"></b-form-input>
        <b-form-datalist id="input-list" :options="listComponent" v-if="this.selected == 3 || this.selected == 4"></b-form-datalist>

        <label v-if="this.selected == 2 || this.selected == 4" id="formComp">Student :</label>
        <b-form-input list="input-list2" id="input-with-list2" v-if="this.selected == 2 || this.selected == 4"></b-form-input>
        <b-form-datalist id="input-list2" :options="listUser" v-if="this.selected == 2 || this.selected == 4"></b-form-datalist>

        <p></p>
        <b-button variant="success" id="formComp">Validate</b-button>
        </div>

        <div id="app">
            <div id="content">
                <canvas ref="chart"></canvas>
            </div>
        </div>
    </div>
</template>

<script>
    import Chart from 'chart.js';

    export default {
        data() {
            return {
                listUser: ['Apple', 'Banana', 'Grape', 'Kiwi', 'Orange'],
                listComponent: ['Module 1', 'Module 2', 'Module 3', 'Module 4', 'Module 5', 'Module 6'],
                dropDownOptions: [
                    { value: 1, text: 'mean by module' },
                    { value: 2, text: 'mean by module by student' },
                    { value: 3, text: 'mean componenents by module' },
                    { value: 4, text: 'mean componenents by module by student' },
                ],
                selected: ''
            }
        },
        name: 'app',
        mounted() {
            var chart = this.$refs.chart;
            var ctx = chart.getContext("2d");
            var myChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ["Module1", "Module2", "Module3", "Module4", "Module5", "Module6"],
                    datasets: [{
                        label: 'Mean in module',
                        data: [50, 75, 66, 30, 89, 42],
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
                                beginAtZero: true
                            }
                        }]
                    }
                }
            });
        }
    }
</script>

<style>
   #contenu {
       text-align: center;
       padding-top: 50px;
       margin: auto;
   }
   #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    #content {
        margin: auto;
        width: 1024px;
        background-color: #FFFFFF;
        padding: 20px;
    }
    #form {
        margin-left: 20%;
        margin-right: 20%;
        background-color: #fff0f0;
        padding: 20px;
        border-radius: 8px;
    }

    #formComp {
        padding-top: 10px;
    }
</style>