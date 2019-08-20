<template>
    <div id="contenu">

        <div id="form">
        <b-form-select v-model="selected" :options="dropDownOptions" id="formComp"></b-form-select>

        <label v-if="this.selected == 3" id="formComp">Module :</label>
        <b-form-input v-model="selectedModule" list="input-list" id="input-with-list" v-if="this.selected == 3 || this.selected == 4"></b-form-input>
        <b-form-datalist id="input-list" :options="modules" v-if="this.selected == 3 || this.selected == 4"></b-form-datalist>

        <label v-if="this.selected == 2" id="formComp">Student :</label>
        <b-form-input v-model="selectedStudent" list="input-list2" id="input-with-list2" v-if="this.selected == 2 || this.selected == 4"></b-form-input>
        <b-form-datalist id="input-list2" :options="listUser" v-if="this.selected == 2 || this.selected == 4"></b-form-datalist>

        <p></p>
        <b-button v-on:click="generateGraph" variant="success" id="formComp">Validate</b-button>
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
    import axios from 'axios';
    export default {
        data() {
            return {
                modules: [],
                listUser: [],
                modulesDict: new Map(),
                userDict: new Map(),
                selectedModule: '',
                selectedStudent: '',
                dropDownOptions: [
                    { value: 1, text: 'mean by module' },
                    { value: 2, text: 'mean by module by student' },
                    { value: 3, text: 'mean components by module' }
                ],
                selected: ''
            }
        },
        name: 'app',
        mounted() {
            var chart = this.$refs.chart;
            var ctx = chart.getContext("2d");
            this.$refs.chart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: [],
                    datasets: [{
                        label: '',
                        data: [],
                        backgroundColor: [
                        ],
                        borderColor: [
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    scales: {
                        yAxes: [{
                            ticks: {
                                beginAtZero: true,
                                max: 100
                            }
                        }]
                    }
                }
            });
        },
    async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get(process.env.frontUrl + "modules", config);
      for(var i=0; i < res.data.length; i++) {
          this.modules.push(res.data[i].title);
          this.modulesDict.set(res.data[i].title, res.data[i].id)
      }

      const res2 = await axios.get(process.env.frontUrl + "users", config);
      for(var j=0; j < res2.data.length; j++) {
          this.listUser.push(res2.data[j].name);
          this.userDict.set(res2.data[j].name, res2.data[j].id)
      }
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
      generateGraph: async function (event) {
          try {
            const config = {
            headers: {
                Accept: "application/json"
            }
            };

            switch(this.selected) {
                case 1:
                    var res2;
                    var listeMean = [];

                    for (i=0; i < this.modules.length; i++) {
                        var moduleID = this.modulesDict.get(this.modules[i]);
                        console.log(moduleID)
                        res2 = await axios.get(process.env.frontUrl + "NoteExams/module/" + moduleID);
                        var listNotesModule = res2.data;

                        listeMean.push(0);
                        var sumCoef = 0;
                        for(var j=0; j < listNotesModule.length; j++) {
                            listeMean[listeMean.length - 1] = Number(listeMean[listeMean.length - 1]) + Number(listNotesModule[j].note) * Number(listNotesModule[j].percentage) / 100;
                            sumCoef += listNotesModule[j].percentage / 100;
                        }
                        listeMean[listeMean.length - 1] = listeMean[listeMean.length - 1] / sumCoef;
                    }
                    
                    var mylabels = this.modules;
                    var myDatas = listeMean;
                    var myColors = [];
                    var myColorsBorder = [];
                    var labelLegend = 'Mean for each module'

                    for(var i=0; i < myDatas.length; i++) {
                        
                        if(myDatas[i] < 50) {
                            myColors.push('rgba(255, 99, 132, 0.2)');
                            myColorsBorder.push('rgba(255,99,132,1)');
                        } else {
                            myColors.push('rgba(75, 192, 192, 0.2)');
                            myColorsBorder.push('rgba(75, 192, 192, 1)');
                        }
                    }
                    this.$refs.chart.data.labels = mylabels;
                    this.$refs.chart.data.datasets[0].backgroundColor = myColors;
                    this.$refs.chart.data.datasets[0].borderColor = myColorsBorder;
                    this.$refs.chart.data.datasets[0].data = myDatas;
                    this.$refs.chart.data.datasets[0].label = labelLegend;
                    this.$refs.chart.update()

                    break;
                case 2:
                    var userID = this.userDict.get(this.selectedStudent);
                    const res = await axios.get(process.env.frontUrl + "NoteExams/user/" + userID, config);
                    var myInfos = res.data.note_exams;
                    console.log(myInfos)
                    var myMap  = new Map();

                    for(var k=0; k < myInfos.length; k++) {
                        if (!myMap.has(myInfos[k].exam.component.modules.title)) {
                            myMap.set(myInfos[k].exam.component.modules.title, 0)
                        }
                        myMap.set(myInfos[k].exam.component.modules.title, (myMap.get(myInfos[k].exam.component.modules.title) + Number(myInfos[k].exam.component.percentage) / 100 * Number(myInfos[k].note)))
                    }
                    mylabels = Array.from(myMap.keys());
                    myDatas = [];
                    myColors = [];
                    myColorsBorder = [];
                    labelLegend = 'Mean in module for ' + this.selectedStudent
                    for(var l=0; l < mylabels.length; l++) {
                        myDatas.push(myMap.get(mylabels[l]));
                        if(myMap.get(mylabels[l]) < 50) {
                            myColors.push('rgba(255, 99, 132, 0.2)');
                            myColorsBorder.push('rgba(255,99,132,1)');
                        } else {
                            myColors.push('rgba(75, 192, 192, 0.2)');
                            myColorsBorder.push('rgba(75, 192, 192, 1)');
                        }
                    }

                    this.$refs.chart.data.labels = mylabels;
                    this.$refs.chart.data.datasets[0].backgroundColor = myColors;
                    this.$refs.chart.data.datasets[0].borderColor = myColorsBorder;
                    this.$refs.chart.data.datasets[0].data = myDatas;
                    this.$refs.chart.data.datasets[0].label = labelLegend;
                    this.$refs.chart.update()
                    break;
                case 3:
                    moduleID = this.modulesDict.get(this.selectedModule);
                    console.log(moduleID)
                    const res3 = await axios.get(process.env.frontUrl + "NoteExams/module/data/" + moduleID, config);
                    var myData = res3.data;
                    console.log(myData)
                    var listMean = []
                    var listComponents = []
                    var mean = 0;
                    for(var m=1; m <= Object.keys(myData).length; m++) {
                        mean = 0;
                        listComponents.push(myData[m].name)
                        for(var z=0; z < myData[m].marks.length; z++) {
                            mean += Number(myData[m].marks[z]);
                        }
                        mean = mean / myData[m].marks.length;
                        listMean.push(mean);
                    }
                    console.log(listMean)

                    mylabels = listComponents;
                    myDatas = listMean;
                    myColors = [];
                    myColorsBorder = [];
                    labelLegend = 'Mean for each component in ' + this.selectedModule

                    for(var i=0; i < listMean.length; i++) {
                        
                        if(listMean[i] < 50) {
                            myColors.push('rgba(255, 99, 132, 0.2)');
                            myColorsBorder.push('rgba(255,99,132,1)');
                        } else {
                            myColors.push('rgba(75, 192, 192, 0.2)');
                            myColorsBorder.push('rgba(75, 192, 192, 1)');
                        }
                    }

                    this.$refs.chart.data.labels = mylabels;
                    this.$refs.chart.data.datasets[0].backgroundColor = myColors;
                    this.$refs.chart.data.datasets[0].borderColor = myColorsBorder;
                    this.$refs.chart.data.datasets[0].data = myDatas;
                    this.$refs.chart.data.datasets[0].label = labelLegend;
                    this.$refs.chart.update()


                    break;
                default:
                    alert('Please, select a chart type')
            }
          } catch(e) {
                console.log(e)
                alert('Missing values')
          }
      }
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