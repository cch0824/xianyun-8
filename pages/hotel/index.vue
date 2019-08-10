<template>
  <div class="hotel-main">
    <!-- 面包屑导航 -->
    <div class="breadcrumb">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item>酒店</el-breadcrumb-item>
        <el-breadcrumb-item>南京市酒店预订</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!-- 住店信息组件 -->
    <div class="stayInfo">
      <StayInfo />
    </div>
    <!-- 景点和地图组件 -->
    <div class="scenicMap">
      <scenicInfo />
    </div>
    <!-- 酒店筛选组件 -->
    <div class="hotelFilter">
      <HotelFilter />
    </div>
    <!-- 酒店列表组件 -->
    <div class="hotelList">
      <HotelItem
        v-for="(item,index) in showHotelList"
        :key="index"
        :data="item"
        :hotelType="item.hoteltype"
        :products="item.products"
        class="hotelItem"
      />
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pageNum"
        :page-sizes="[4, 6, 8, 10]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
      ></el-pagination>
    </div>
  </div>
</template>
<script>
import StayInfo from "@/components/hotel/stayInfo";
import scenicInfo from "@/components/hotel/scenicInfo";
import HotelFilter from "@/components/hotel/hotelFilter";
import HotelItem from "@/components/hotel/hotelItem";
export default {
  components: {
    StayInfo,
    scenicInfo,
    HotelFilter,
    HotelItem
  },
  data() {
    return {
      hotelData: [],
      hotelList: [],
      // 更改分页数据是渲染的酒店列表数据
      showHotelList: [],
      // 每一个酒店的信息
      hotel: {},
      total: 0,
      // 当前页
      pageNum: 1,
      pageSize: 4
    };
  },
  methods: {
    showHotel() {
      //
      this.showHotelList = this.hotelList.slice(
        (this.pageNum - 1) * this.pageSize,
        this.pageNum * this.pageSize
      );
    },
    handleSizeChange(val) {
      this.pageSize = val;
      this.showHotel()
    },
    handleCurrentChange(val) {
      this.pageNum = val;
      this.showHotel()
    }
  },
  mounted() {
    this.$axios({
      url: "/hotels"
    }).then(res => {
      this.hotelData = res.data.data;
    });

    this.$axios({
      url: "/hotels"
    }).then(res => {
      console.log(res, 520);
      this.hotelList = res.data.data;
      this.total = res.data.data.length
      this.showHotel()
    });
  }
};
</script>
<style lang="less" scoped>
.hotel-main {
  width: 1000px;
  margin: 0 auto;
  .breadcrumb {
    padding: 20px 0;
  }
  .stayInfo {
    margin-bottom: 30px;
  }
  .scenicMap {
    margin-bottom: 30px;
  }
  .hotelFilter {
    margin-bottom: 30px;
  }
  .hotelList {
    margin-bottom: 10px;
    .hotelItem {
      margin-bottom: 50px;
    }
  }
}
</style>
