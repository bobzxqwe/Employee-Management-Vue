<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts-wordcloud')
require('echarts/theme/macarons') // echarts theme
import { debounce } from '@/utils'
export default {
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '300px'
    }
  },
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    this.initChart()
    this.__resizeHandler = debounce(() => {
      if (this.chart) {
        this.chart.resize()
      }
    }, 100)
    window.addEventListener('resize', this.__resizeHandler)
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    window.removeEventListener('resize', this.__resizeHandler)
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')
      const data = [{
        'name': 'JAVA',
        'value': 1446
      },
      {
        'name': 'C++',
        'value': 928
      },
      {
        'name': 'C#',
        'value': 906
      },
      {
        'name': 'HTML',
        'value': 825
      },
      {
        'name': 'Fortran',
        'value': 514
      },
      {
        'name': 'ALGOL',
        'value': 486
      },
      {
        'name': 'BASIC',
        'value': 53
      },
      {
        'name': 'PYTHON',
        'value': 163
      },
      {
        'name': 'PHP',
        'value': 86
      },
      {
        'name': 'HTML5',
        'value': 17
      },
      {
        'name': 'JavaScript',
        'value': 6
      },
      {
        'name': 'CSS',
        'value': 1
      },
      {
        'name': 'SPRINGBOOT',
        'value': 1437
      },
      {
        'name': 'RUBY',
        'value': 422
      },
      {
        'name': 'VB',
        'value': 353
      },
      {
        'name': 'GO',
        'value': 331
      },
      {
        'name': 'SQL',
        'value': 313
      },
      {
        'name': 'MATLAB',
        'value': 307
      },
      {
        'name': 'NodeJS',
        'value': 43
      },
      {
        'name': 'MongoDB',
        'value': 15
      },
      {
        'name': 'Redis',
        'value': 438
      },
      {
        'name': 'MariaDB',
        'value': 957
      },
      {
        'name': 'WWW',
        'value': 927
      },
      {
        'name': 'Machine Learning',
        'value': 908
      },
      {
        'name': 'Web',
        'value': 693
      },
      {
        'name': 'Layui',
        'value': 611
      },
      {
        'name': 'VUE',
        'value': 512
      },
      {
        'name': 'React',
        'value': 382
      }]
      this.chart.setOption({
        backgroundColor: '#fff',
        tooltip: {
          show: false
        },
        series: [{
          type: 'wordCloud',
          gridSize: 1,
          sizeRange: [12, 55],
          rotationRange: [-45, 0, 45, 90],
          textStyle: {
            normal: {
              color: function() {
                return 'rgb(' +
                  Math.round(Math.random() * 255) +
                  ', ' + Math.round(Math.random() * 255) +
                  ', ' + Math.round(Math.random() * 255) + ')'
              }
            }
          },
          left: 'center',
          top: 'center',
          right: null,
          bottom: null,
          data: data
        }]
      })
    }
  }
}
</script>
