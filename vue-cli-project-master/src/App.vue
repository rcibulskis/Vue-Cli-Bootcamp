<template>
  <div id="app"  v-bind:style="overall_container">
    <navbar>
      <div slot="buttons">
        <dropdown :navbar="navbar" :headertext="headertext1"></dropdown>
        <dropdown :navbar="subreddits" :headertext="headertext2"></dropdown>
      </div>
    </navbar>
        <div class="jumbotron" v-bind:style="style_container_header">
            <div class="container">
                <h1 class="display-12">Data Tools Bootcamp</h1>
            </div>
            <div class="container">
                    <div class="container" v-bind:style="style_container">
        <div class="row">
            <div class="col-xs-12" v-bind:style="style_graph">
  <chart></chart>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import chart from './components/Chart.vue'
import Navbar from './components/Navbar.vue'
import Navbar1 from './components/Navbar1.vue'

export default {
  name: 'app',
  components: {chart: chart, navbar: Navbar, dropdown: Navbar1},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      global_sales: [],
      na_sales: [],
      label: [],
      ratingslabel: [],
      criticalscore: [],
      criticscore: [],
      genrelabel: [],
      ratingsArray: [],
      genreArray: [],
      salesArray: [],
      headertext1: 'Gaming Sites',
      headertext2: 'Subreddit Sites',
      navbar: {'IGN': 'https://www.ign.com', 'GameSpot': 'https://www.gamespot.com'},
      subreddits: {'r/gaming': 'https://www.reddit.com/r/gaming', 'r/PS4': 'https://www.reddit.com/r/ps4', 'r/Switch': 'https://www.reddit.com/r/switch'},
      gamingsites: {'gamingsites': {'IGN': 'https://www.ign.com', 'GameSpot': 'https://www.gamespot.com'}, 'subreddits': {'r/Gaming': 'https://reddit.com/r/gaming', 'r/PS4': 'https://reddit.com/r/ps4'}},
      testdata: '{"genre":{"critic_score":{"Role-Playing":71,"Puzzle":67.28571428571429,"Shooter":67.35416666666667,"Misc":63.654545454545456,"Fighting":67.02083333333333,"Simulation":65.35593220338983,"Platform":67.48698884758365,"Strategy":69.34426229508196,"Adventure":62.34108527131783,"Action":62.401041666666664,"Sports":69.01712328767124,"Racing":62.2962962962963}},"ratings":{"critic_score":{"E10+":64.34189723320158,"M":69,"E":65.41368584758942,"T":67.10223048327137}},"sales":{"na_sales":{"N64":139.02000000000015,"GBA":187.54000000000033,"3DS":83.48999999999992,"Wii":496.8999999999991,"NES":125.94000000000005,"GC":133.46000000000004,"GB":114.32000000000001,"WiiU":38.10000000000003,"SNES":61.22999999999998,"DS":382.6699999999979},"global_sales":{"N64":218.87999999999985,"GBA":318.499999999998,"3DS":259.0899999999991,"Wii":908.129999999998,"NES":251.06999999999988,"GC":199.3600000000007,"GB":255.44999999999987,"WiiU":82.16000000000003,"SNES":200.05000000000024,"DS":807.0999999999868}}}',
      publishers: ['Nintendo', 'Sony', 'Microsoft'],
      publisherselected: 'Nintendo',
      include: 'True',
      gaming: [],
      style_container: {
        backgroundColor: '#D5D5D5',
        width: '80%'
      },
      style_container_header: {
        backgroundColor: '#D5D5D5'
      },
      overall_container: {
        backgroundColor: '#96858F'
      },
      style_graph: {
        color: 'white',
        width: '80%'
      }
    }
  },
  mounted () {
    this.postNow()
  },
  methods: {
    postNow: function () {
      var self = this
      axios.post('../default/get_data', {
        publisherselected: this.publisherselected
      })
        .then(function (response) {
          self.processdata(response)
        })
        .catch((error) => {
          self.processdata({data: JSON.parse(this.testdata)})
          console.log(error)
        })
    },
    processdata: function (response) {
      var _this = this
      var sales = response.data.sales
      var ratings = response.data.ratings
      var genre = response.data.genre
      var label = []
      var globalsales = []
      var nasales = []
      var ratingslabel = []
      var criticalscore = []
      var criticscore = []
      var genrelabel = []

      for (var x in sales.globalsales) {
        label.push(x)
      }

      for (var i in label) {
        globalsales.push(sales['global_sales'][label[i]])
        nasales.push(sales['na_sales'][label[i]])
      }

      for (var j in ratings.critic_score) {
        ratingslabel.push(j)
      }

      for (var k in ratingslabel) {
        criticalscore.push(ratings['critic_score'][ratingslabel[k]])
      }

      for (var b in genre.critic_score) {
        genrelabel.push(b)
      }

      for (var q in genrelabel) {
        criticscore.push(genre['critic_score'][genrelabel[q]])
      }

      _this.label = label
      _this.globalsales = globalsales
      _this.nasales = nasales
      _this.ratingslabel = ratingslabel
      _this.criticalscore = criticalscore
      _this.criticscore = criticscore
      _this.genrelabel = genrelabel

      _this.ratingsArray = [{
        label: 'Average critic score per ESRB ratings',
        backgroundColor: '#6D7993',
        data: _this.criticalscore
      }]

      _this.genreArray = [{
        label: 'Average critic score per genre',
        backgroundColor: '#6D7993',
        data: _this.criticscore
      }]

      _this.salesArray = [{
        label: 'Global Sales in units sold',
        backgroundColor: '#6D7993',
        data: _this.global_sales
      },
      {
        label: 'North America Sales in units sold',
        backgroundColor: '#9099A2',
        data: _this.nasales
      }
      ]
    }
  }
}
</script>

