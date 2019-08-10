<template>
  <div class="hotel-filter">
    <el-row class="filterClassify">
      <el-col :span="4">
        <el-row type="flex" justify="space-between">
          <span>价格</span>
          <span>0-{{value}}</span>
        </el-row>
        <el-row>
          <el-slider v-model="value" :max="4000"></el-slider>
        </el-row>
      </el-col>

      <el-col :span="5">
        <el-row >
          <span>住宿等级</span>
        </el-row>
        <el-row>
          <el-select v-model="levels" placeholder="请选择" class="filterSelect" @change="handleLevelsFilter">
            <el-option
              v-for="item in hotelType.levels"
              :key="item.id"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-row>
      </el-col>

      <el-col :span="5">
        <el-row >
          <span>住宿类型</span>
        </el-row>
        <el-row>
          <el-select v-model="type" placeholder="请选择" class="filterSelect">
            <el-option
              v-for="item in hotelType.types"
              :key="item.id"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-row>
      </el-col>

      <el-col :span="5">
        <el-row >
          <span>酒店设施</span>
        </el-row>
        <el-row>
          <el-select v-model="assets" placeholder="请选择" class="filterSelect" multiple collapse-tags>
            <el-option
              v-for="item in hotelType.assets"
              :key="item.id"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-row>
      </el-col>

      <el-col :span="5">
        <el-row >
          <span>酒店品牌</span>
        </el-row>
        <el-row>
          <el-select v-model="brand" placeholder="请选择" class="filterSelect">
            <el-option
              v-for="item in hotelType.brands"
              :key="item.id"
              :label="item.name"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: 0,
      hotelType: {},  // 酒店数据
      levels:'',
      assets:'',
      brand:'',
      type:[]
    };
  },
  mounted() {
    this.$axios({
      url: "/hotels/options"
    }).then(res => {
      console.log(res);
      this.hotelType = res.data.data;
    });
  },
  methods:{
    handleLevelsFilter(value){
      
    }
  }
};
</script>
<style lang="less" scoped>
.filterClassify {
  padding: 10px 20px;
  border: 1px solid #eaeaea;
  div {
    font-size: 14px;
    padding-right: 10px;
  }
  .el-icon--right {
    margin-left: 50px;
  }
}

.filterSelect {
  /deep/.el-input__inner {
    outline: none;
    border: none;
  }
}
</style>
