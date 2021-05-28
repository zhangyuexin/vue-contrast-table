<template>
  <div class="content">
    <el-table
      :data="targetArr"
      :show-header="false"
      stripe
      border
      style="width: 100%"
    >
      <el-table-column
        prop="00"
        align="center"
      />
      <el-table-column
        v-for="item in clumnArr"
        :key="item"
        :prop="String(item)"
        align="center"
      >
        <template slot-scope="scope">
          <div v-if="scope.row['00'] === '图片'">
            <img :src="scope.row[scope.column.property]" alt="">
          </div>

          <span v-else>{{ scope.row[scope.column.property] }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'Contrast',
  props: ['contrast', 'column'],
  data () {
    return {
      targetArr: [],
      clumnArr: []
    }
  },
  created () {
    this.getChangeData()
  },
  methods: {
    getChangeData () {
      const clumnArr = [...new Array(this.contrast.length).keys()] // 改变数据，根据数据的长度生成数组，作为table的column的prop
      const targetArr = [] // 数据数组
      /**
       * 下面则是将原数组转为合适数据
      */
      const tableData = []
      let objKey = []

      // 第一步将原数组中对象的key变为左侧需要展示的文字
      this.contrast.forEach(ele => {
        const obj = {}
        this.column.forEach(item => {
          obj[item.label] = ele[item.prop]
        })
        Object.keys(obj).forEach((item) => {
          objKey.push(item)
        })
        tableData.push(obj)
      })

      // 将所有的key值放到数组中
      objKey = [...new Set(objKey)]

      // 根据左侧值遍历数组
      for (let i = 0; i < objKey.length; i++) {
        const obj = {}
        for (let m = 0; m < tableData.length; m++) {
          obj[m] = tableData[m][objKey[i]]
        }
        targetArr.push(obj)
      }

      // 新增一个00作为左侧第一列的prop
      targetArr.forEach((ele, index) => {
        ele['00'] = objKey[index]
      })

      this.targetArr = targetArr
      this.clumnArr = clumnArr
    }
  }

}
</script>

<style scoped>
.content{
  width: 100%;
  position: relative;
}

</style>
