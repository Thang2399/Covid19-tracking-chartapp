<template>
  <div>
    <h1>Covid-19 tracking chart</h1>
    <div v-if="positiveArr.length > 0 && negativeArr.length > 0">
      <h1>Positive & Negative</h1>
      <LineChart
          label1="Positive" label2="Negative"
          :chartData1="positiveArr" :chartData2="negativeArr"
          :chartColors1="positiveColors" :chartColors2="negativeColors"
          :options="options"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import LineChart from "@/components/linechart/LineChart";

export default {
  name: "LineChartComponent",
  components: {LineChart},
  data() {
    return {
      positiveArr: [],
      positiveColors: {
        borderColor: '#ea5454',
        pointBorderColor: '#ffffff',
        pointBackgroundColor: '#fd0000'
      },
      negativeArr: [],
      negativeColors: {
        borderColor: '#87eca1',
        pointBorderColor: '#ffffff',
        pointBackgroundColor: '#4c915c'
      },
      deathArr: [],
      recoveredArr: [],
      options: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
// created: run code after an instance is created
  async created() {
    const {data} = await axios.get("https://api.covidtracking.com/v1/states/current.json");
    console.log(data);
    data.forEach(item => {
      const {state, death, negative, positive, recovered} = item;

      this.positiveArr.push({state, total: positive})
      this.negativeArr.push({state, total: negative})
      this.deathArr.push({state, total: death})
      this.recoveredArr.push({state, total: recovered})
    })
  }
}
</script>
