<template>
  <div class="content">
    <h2>使用elementUi 的table来实现类似于汽车之家的对比功能，数据格式与平常使用一致</h2>
    <div class="yes-sir">
      <contrastComp :contrast="contrast" :column="column" />
    </div>
  </div>
</template>

<script>

import contrastComp from '@/components/contrast'

const contrast = Object.freeze([
  {
    img: require('../assets/1.jpg'),
    label: '汉兰达 2013款  2.7L 两驱5座紫金版',
    marketTime: '2013.06',
    width_height_length: '4795*1910*1760'
  },
  {
    img: require('../assets/2.jpg'),
    label: '汉兰达 2013款 2.7L 两驱7座紫金版',
    marketTime: '2013.06',
    width_height_length: '4795*1910*1760'
  },
  {
    img: require('../assets/3.jpg'),
    label: '汉兰达 2013款 2.7L 两驱7座探索版',
    marketTime: '2013.07',
    width_height_length: '4795*1910*1760'
  },
  {
    img: require('../assets/4.jpg'),
    label: '汉兰达 2012款 2.7L 两驱5座精英版',
    marketTime: '2012.06',
    width_height_length: '4795*1910*1730'
  }
])

const column = Object.freeze([
  {
    label: '图片',
    prop: 'img'
  },
  {
    label: '名称',
    prop: 'label'
  },
  {
    label: '上市时间',
    prop: 'marketTime'
  },
  {
    label: '长*宽*高(mm)',
    prop: 'width_height_length'
  }
])

export default {
  name: 'Index',
  components: {
    contrastComp
  },
  data () {
    return {
      contrast, // 对比数据，与平时使用相同
      column// 左侧名称和顺序
    }
  }
}
</script>

<style scoped>
.content{
  width: 100%;
}

.yes-sir{
  width: 1000px;
  margin: 30px auto;
  border:solid 1px #eee;
}
</style>
