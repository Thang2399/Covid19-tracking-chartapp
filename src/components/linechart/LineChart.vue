<script>
import {Line} from 'vue-chartjs';

export default {
  extends: Line,
  props: {
    label1: {type: String},
    chartData1: {type: Array},
    chartColors1: {type: Object},

    label2: {type: String},
    chartData2: {type: Array},
    chartColors2: {type: Object},
    options: {type: Object}
  },
  mounted() {
    const states = this.chartData1.map(item => item.state);
    const total1 = this.chartData1.map(item => item.total);
    const total2 = this.chartData2.map(item => item.total);

    const {borderColor1, pointBackgroundColor1} = {
      ...this.chartColors1,
      borderColor1: this.chartColors1.borderColor,
      pointBorderColor1: this.chartColors1.pointBackgroundColor,
      pointBackgroundColor1: this.chartColors1.pointBackgroundColor
    };
    const {borderColor2, pointBackgroundColor2} = {
      ...this.chartColors2,
      borderColor2: this.chartColors2.borderColor,
      pointBorderColor2: this.chartColors1.pointBackgroundColor,
      pointBackgroundColor2: this.chartColors2.pointBackgroundColor
    };

    this.renderChart({
      labels: states,
      datasets: [{
        label: this.label1,
        data: total1,
        fill: false,
        borderColor: borderColor1,
        pointBorderColor: pointBackgroundColor1,
        pointBackgroundColor: pointBackgroundColor1
      }, {
        label: this.label2,
        data: total2,
        fill: false,
        borderColor: borderColor2,
        pointBorderColor: pointBackgroundColor2,
        pointBackgroundColor: pointBackgroundColor2
      }]
    }, this.options)
  }
}
</script>
