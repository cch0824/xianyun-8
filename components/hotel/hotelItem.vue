<template>
  <div class="conser">
    <el-row :gutter="20">
      <!-- 酒店图片 -->
      <el-col :span="8">
        <div class="box1">
          <img :src="`${data.photos}`" alt style="width:320px;height:210px" />
        </div>
      </el-col>
      <!-- 酒店信息 -->
      <el-col :span="10">
        <div class="box2">
          <h4>
            <a href="#">{{data.name}}</a>
          </h4>

          <div class="hao">
            <span>{{data.alias}}</span>
            <span>
              <i class="el-icon-trophy" style="color:#f7ba2a"></i>
              <i class="el-icon-trophy" style="color:#f7ba2a"></i>
              <i class="el-icon-trophy" style="color:#f7ba2a"></i>
            </span>
            <span>{{hotelType.name}}</span>
          </div>

          <!-- 评分栏 -->
          <div class="pingfen">
            <el-rate
              v-model="value"
              disabled
              show-score
              text-color="#ff9900"
              score-template="{value}分"
            ></el-rate>
            <div class="tiao">
              <span>{{data.all_remarks}}</span>条评价
            </div>
            <div class="pian">
              <span>{{data.common_remarks}}</span>篇游记
            </div>
          </div>
          <!-- 地址信息 -->
          <div class="site">
            <i class="el-icon-location"></i>
            位于: {{data.address}}
          </div>
        </div>
      </el-col>
      <!-- 订房网站 -->
      <el-col :span="6">
        <ul>
          <li
            style="padding-bottom:10px;margin-bottom:10px;border-bottom:1px solid #eee;"
            v-for="(item,index) in products"
            :key="index"
          >
            <nuxt-link to="#" style="display:flex;justify-content:space-between">
              <span>{{item.name}}</span>
              <span>
                <i style="color:#ff9900">￥{{item.price}}</i>
                <i style="font-size:14px">起</i>
                <i class="el-icon-arrow-right" style="margin-left:10px"></i>
              </span>
            </nuxt-link>
          </li>
        </ul>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  // 接受index.vue传来对应数据
  props: {
    data: {
      type: Object,
      default: {}
    },
    // 酒店类型
    hotelType: {
      type: Object,
      default: {}
    },
    products: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      value: this.data.stars,
      tableData: this.products
    };
  }
};
</script>


<style lang="less" scoped>
.conser {
  width: 1000px;
  margin: 0 auto;
}
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
// 中间栏
.box2 {
  h4 {
    a {
      color: initial;
      font-weight: 400;
      font-size: x-large;
    }
  }
  .hao {
    color: #999;
    font-size: 16px;
    margin-top: 5px;
    margin-bottom: 10px;
    span {
      .iconfont {
        color: #ff9900;
      }
    }
  }
  .pingfen {
    display: flex;
    height: 30px;
    padding: 5px;
    margin: 0 -5px;
    margin-bottom: 10px;
    box-sizing: border-box;
    .tiao {
      float: left;
      padding-left: 20px;
      span {
        color: #f7ba2a;
      }
    }
    .pian {
      float: left;
      padding-left: 40px;
      span {
        color: #f7ba2a;
      }
    }
  }
  .site {
    font-size: 14px;
    color: #666;
  }
}
// 右侧边栏
.box3 {
  padding: 0 10px;
}

.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
</style>
