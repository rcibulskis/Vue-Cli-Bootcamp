<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  mounted: function () {
    this.renderChart({
      labels: ['Role-Playing', 'Puzzle', 'Shooter', 'Misc', 'Fighting', 'Simulation', 'Platform', 'Strategy', 'Adventure', 'Action', 'Sports', 'Racing'],
      datasets: [
        {
          label: 'Critic Score',
          backgroundColor: '#f87979',
          data: [71, 67.28571428571429, 67.35416666666667, 63.654545454545456, 67.02083333333333, 65.35593220338983, 67.48698884758365, 69.34426229508196, 62.34108527131783, 62.401041666666664, 69.01712328767124, 62.2962962962963]
        }
      ]
    })
  }
}
</script>
