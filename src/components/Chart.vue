<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  props: ["countrydata"],
  data: () => ({
    deathsColor: "#f00",
    confirmedColor: "#036",
    recoveredColor: "#053",
    options: {
      responsive: true,
      maintainAspectRatio: false,
      aspectRatio: 0.5,
      tooltips: {
        mode: "index",
        position: "cursor",
        intersect: false
      },
      scales: {
        xAxes: [
          {
            gridLines: {
              borderDash: [1, 3],
              color: "rgba(221, 221, 221, 0.65)",
              z: 1
            }
          }
        ],
        yAxes: [
          {
            gridLines: {
              borderDash: [1, 3],
              color: "rgba(221, 221, 221, 0.65)",
              z: 1
            }
          }
        ]
      }
    }
  }),
  mounted() {
    this.renderChart(this.chartdata, this.options);
    this.$nextTick().then(() => this.resizeChart());
    window.Chart.Tooltip.positioners.cursor = function(
      chartElements,
      coordinates
    ) {
      return coordinates;
    };
    window.Chart.defaults.global.elements.point.hitRadius = 3;
    window.Chart.defaults.global.elements.point.hoverRadius = 6;
    window.Chart.defaults.global.elements.point.borderWidth = 2;
  },
  computed: {
    activeCount() {
      return this.getActive(this.lastDay);
    },
    lastDay() {
      return this.countrydata[this.countrydata.length - 1];
    },
    chartdata() {
      return {
        labels: this.countrydata.map(day => day.date),
        datasets: [
          {
            label: `Mortes (${this.lastDay.deaths})`,
            data: this.countrydata.map(day => ({
              x: day.date,
              y: day.deaths || null
            })),
            borderColor: this.deathsColor,
            backgroundColor: "#FFF0",
            pointBackgroundColor: "#fff"
          },
          {
            label: `Recuperados (${this.lastDay.recovered})`,
            data: this.countrydata.map(day => ({
              x: day.date,
              y: day.recovered || null
            })),
            borderColor: this.recoveredColor,
            pointBackgroundColor: "#fff",
            backgroundColor: this.recoveredColor + "6"
          },
          {
            label: `Confirmados (${this.lastDay.confirmed})`,
            data: this.countrydata.map(day => ({
              x: day.date,
              y: day.confirmed || null
            })),
            borderColor: this.confirmedColor,
            pointBackgroundColor: "#fff",
            backgroundColor: this.confirmedColor + "c"
          },
          {
            label: `Activos (${this.activeCount})`,
            borderColor: "#eee",
            backgroundColor: "transparent",
            pointBackgroundColor: "#fff",
            data: this.countrydata.map(day => ({
              x: day.date,
              y: this.getActive(day)
            }))
          }
        ]
      };
    }
  },
  methods: {
    getActive(day) {
      return day.confirmed - day.deaths - day.recovered;
    },
    resizeChart() {
      this.$refs.canvas.parentNode.style.height = "calc(100vh - 180px)";
      this.$refs.canvas.parentNode.style.width = "calc(100vw - 30px)";
    }
  },
  watch: {
    countrydata: function() {
      this.renderChart(this.chartdata, this.options);
    }
  }
};
</script>
