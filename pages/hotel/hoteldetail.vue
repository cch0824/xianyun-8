<template>
  <!-- 酒店详情页开始 -->
  <div class="houteldetail main">
    <!-- 面包屑导航开始 -->
    <el-breadcrumb separator=">" class="houtelHeader">
      <el-breadcrumb-item :to="{ path: '/houtel' }">酒店</el-breadcrumb-item>
      <el-breadcrumb-item>
        <a href="/houtel">南京酒店</a>
      </el-breadcrumb-item>
      <el-breadcrumb-item>好来商务酒宾馆</el-breadcrumb-item>
    </el-breadcrumb>

    <el-row class="haolaiHotelrow">
      <span class="haolaiHotelSpan">好来商务酒宾馆</span>
      <i class="iconfont iconhuangguan"></i>
      <i class="iconfont iconhuangguan"></i>
      <i class="iconfont iconhuangguan"></i>
      <i class="iconfont iconhuangguan"></i>
      <i class="iconfont iconhuangguan"></i>
    </el-row>
    <span>hao lai ge shang wu hotel</span>

    <el-row class="gaocunxianZhen">
      <i class="el-icon-location"></i>
      <span>高淳县淳溪镇镇兴路118号(高淳县委党校对面)</span>
    </el-row>
    <!-- 面包屑导航结束 -->

    <!-- 房型图片开始 -->
    <el-row type="flex" class="row-bg">
      <el-col :span="12">
        <div class="grid-content1 bg-purple">
          <img src="http://157.122.54.189:9093/images/hotel-pics/5.jpeg" alt />
        </div>
      </el-col>

      <el-col :span="12" class="houseImgright">
        <div class="grid-content2 bg-purple-light">
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/1.jpeg" alt />
          </a>
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/2.jpeg" alt />
          </a>
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/3.jpeg" alt />
          </a>
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/5.jpeg" alt />
          </a>
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/4.jpeg" alt />
          </a>
          <a href>
            <img src="http://157.122.54.189:9093/images/hotel-pics/6.jpeg" alt />
          </a>
        </div>
      </el-col>
    </el-row>
    <!-- 房型图片结束 -->

    <!-- Tab详情开始 -->
    <el-table :data="Tabdata" style="width: 100%" class="tab-tabdetail">
      <el-table-column label="价格来源" prop="pricename" width="330"></el-table-column>
      <el-table-column label="低价房型" prop="smallhouse" width="530"></el-table-column>
      <el-table-column label="最低价格/每晚" prop="lowpricehouse" width="130"></el-table-column>
    </el-table>
    <!-- Tab详情结束 -->

    <!-- 地图开始 -->
    <!-- 地图 -->
    <el-row type="flex" class="row-bg">
      <el-col :span="12">
        <div id="container"></div>
      </el-col>

      <!-- 地图导航 -->
      <el-col :span="12" class="mapRight">
        <el-tabs @tab-click="handleClick">
          <!-- 风景 -->
          <el-tab-pane label="风景" name="first" v-show="dianji===1">
            <ul class="infinite-list" v-infinite-scroll="load" style="overflow:auto">
              <li
                v-for="(item,index) in count"
                :key="index"
                style="margin:20px 0;"
                class="infinite-list-item"
              >
                <span>{{ item.name }}</span>
                <span style="margin-left:80px;">{{ item.number }}</span>
              </li>
            </ul>
          </el-tab-pane>
          <!-- 交通 -->
          <el-tab-pane label="交通" name="second">
            <ul class="infinite-list" v-infinite-scroll="load" style="overflow:auto">
              <li
                v-for="(item,index) in count2"
                :key="index"
                style="margin:20px 0;fontSize:14px;"
                class="infinite-list-item"
              >
                <span>{{ item.name }}</span>
                <span style="margin-left:80px;">{{ item.number }}</span>
              </li>
            </ul>
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
    <!-- 地图结束 -->

    <!-- 基本信息开始 -->
    <div>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">基本信息</div>
        </el-col>
        <el-col :span="18">
          <div class="grid-content bg-purple-light">
            入住时间: 14:00之后 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            离店时间: 12:00之前&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            2010年开业 / 2015年装修&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            酒店规模: 148间客房
          </div>
        </el-col>
      </el-row>
      <!-- 分隔符 -->
      <el-divider></el-divider>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">主要设施</div>
        </el-col>
        <el-col :span="18">
          <div class="grid-content bg-purple-light">
            <span>外币兑换服务</span> &nbsp;&nbsp;
            <span>电梯</span> &nbsp;&nbsp;
            <span>洗衣</span>&nbsp;&nbsp;
            <span>服务</span>&nbsp;&nbsp;
            <span>热水壶</span>
          </div>
        </el-col>
      </el-row>
      <el-divider></el-divider>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">停车服务</div>
        </el-col>
        <el-col :span="18">
          <div class="grid-content bg-purple-light">-</div>
        </el-col>
      </el-row>
      <el-divider></el-divider>
      <el-row>
        <el-col :span="6">
          <div class="grid-content bg-purple">品牌信息</div>
        </el-col>
        <el-col :span="18">
          <div class="grid-content bg-purple-light">-</div>
        </el-col>
      </el-row>
      <el-divider></el-divider>
    </div>
    <!-- 基本信息结束 -->

    <!-- 底部评论开始 -->
    <div class="userMement-one">
      <div class="userRec">
        <div class="usercomment-top">
          <span>0条用户真实用户评论</span>
        </div>
      </div>
      <div class="box">
        <el-row :gutter="20">
          <el-col :span="4">
            <div class="grid-content bg-purple">
              <p>总评数：9</p>
              <p>好评数：1</p>
              <p>差评数：2</p>
            </div>
          </el-col>
          <el-col :span="8">
            <el-rate
              v-model="value5"
              disabled
              show-score
              text-color="#ff9900"
              score-template="{value}分"
            ></el-rate>
            <div class="tuijian">推荐</div>
          </el-col>
          <el-col :span="4">
            <div class="grid-content bg-purple">环境</div>
          </el-col>
          <el-col :span="4">
            <div class="grid-content bg-purple">产品</div>
          </el-col>
          <el-col :span="4">
            <div class="grid-content bg-purple">服务</div>
          </el-col>
        </el-row>
      </div>
    </div>
    <!-- 底部评论结束 -->

    
  </div>
  <!-- 酒店详情页结束 -->
</template>

<script>
export default {
  data() {
    return {
      //点击触发地图tab栏
      handleClick() {},
      load() {},
      // tab栏切换地图导航
      dianji: 1,
      count: [
        { name: "高淳老街", muber: "1.03公里" },
        { name: "红太阳广场", muber: "0.60公里" },
        { name: "甘霖广场", muber: "0.15公里" },
        { name: "跬步居", muber: "1.12公里" },
        { name: "凤岭公园", muber: "0.28公里" },
        { name: "红宝丽广场", muber: "0.37公里" },
        { name: "人民广场", muber: "1.96公里" },
        { name: "高淳婚礼文化广场", muber: "0.63公里" },
        { name: "红红的太阳", muber: "0.58公里" },
        { name: "泮池园", muber: "0.76公里" }
      ],
      count2: [
        { name: "甘霖路口(公交站)", muber: "0.09公里" },
        { name: "凤岭公园(公交站)", muber: "0.24公里" },
        { name: "停车场(镇兴大厦西南)", muber: "0.01公里" },
        { name: "镇兴大厦停车场", muber: "0.12公里" },
        { name: "高淳(地铁站)", muber: "0.26公里" },
        { name: "停车场(镇兴大厦西)", muber: "0.86公里" },
        { name: "怡城花园(公交站)", muber: "0.16公里" },
        { name: "停车场(甘霖路)", muber: "0.25公里" },
        { name: "停车场(牡丹路)", muber: "0.36公里" },
        { name: "停车场(春泉路)", muber: "0.12公里" }
      ],
      value5: 3.5,
      // tab栏详情信息
      Tabdata: [
        {
          pricename: "携程",
          smallhouse: "高级大床房A",
          lowpricehouse: "¥137起"
        },
        {
          pricename: "艺龙",
          smallhouse: "高级大床房A",
          lowpricehouse: "¥137起"
        },
        {
          pricename: "Houtels",
          smallhouse: "高级大床房A",
          lowpricehouse: "¥137起"
        }
      ]
    };
  },

  mounted() {
    //导入地图
    window.onLoad = function() {
      var map = new AMap.Map("container", {
        zoom: 11, //级别
        center: [118.8718107, 31.32846821], //中心点坐标
        viewMode: "3D" //使用3D视图
      });
    };

    var url =
      "https://webapi.amap.com/maps?v=1.4.15&key=8205e8295ae64dd2d94937ea12091506&callback=onLoad";
    var jsapi = document.createElement("script");
    jsapi.charset = "utf-8";
    jsapi.src = url;
    document.head.appendChild(jsapi);

    window.onLoad = function() {
      var map = new AMap.Map("container", {
        zoom: 11, //级别
        center: [118.8718107, 31.32846821], //中心点坐标
        viewMode: "3D" //使用3D视图
      });

      // 创建一个 Marker 实例：
      var marker = new AMap.Marker({
        position: new AMap.LngLat(118.8718107, 31.32846821), // 经纬度对象，也可以是经纬度构成的一维数组[116.39, 39.9]
        title: "广州"
      });

      // 将创建的点标记添加到已有的地图实例：
      map.add(marker);
    };
  }
};
</script>

<style scoped lang='less'>
/* 面包屑开始 */
.houtelHeader {
  margin-top: 10px;
}
.main {
  width: 1000px;
  margin: 0 auto;
}
.iconfont {
  color: #ff9b00;
}
.haolaiHotelSpan {
  font-size: 25px;
}
.haolaiHotelrow {
  margin-top: 20px;
  margin-bottom: 5px;
}
.gaocunxianZhen {
  margin-bottom: 50px;
}
/* 面包屑结束 */

/* 房型图片开始 */
.row-bg {
  margin-bottom: 50px;
}
.grid-content1 img {
  height: 360px;
  width: 640px;
}
.grid-content2 img {
  width: 170px;
}
.houseImgright {
  margin-left: 155px;
}
.tab-tabdetail {
  margin-bottom: 30px;
}
/* 房型图片结束 */

/* 地图开始 */
#container {
  width: 650px;
  height: 360px;
}
.mapRight {
  width: 300px;
  height: 300px;
  margin-left: 175px;
}
.infinite-list {
  height: 240px;
}
/* 地图结束 */

/* 基本信息开始 */
.bg-purple-light span {
  background: #eeeeee;
  padding: 6px;
  border-radius: 3%;
}
/* 基本信息结束 */

/* 用户评论开始 */
.box {
  width: 1000px;
  margin: 0 auto;
  .el-row {
    margin-bottom: 20px;
    color: #f7ba2a;
    font-weight: 500;
    margin-left: 5px;
    .el-rate {
      margin-top: 40px;
    }
    &:last-child {
      margin-bottom: 0;
      margin-top: 30px;
      p {
        color: #6b6d83;
        font-size: 16px;
      }
    }
  }
  .el-col {
    border-radius: 4px;
    &:nth-child(2) {
      position: relative;
      .tuijian {
        position: absolute;
        top: 8px;
        left: 13%;
        width: 80px;
        height: 80px;
        line-height: 75px;
        font-size: 30px;
        border-radius: 50px;
        border: 3px solid #f7ba2a;
        opacity: 0.3;
        color: #f7ba2a;
        transform: rotate(-35deg);
      }
    }
    &:nth-child(n + 2) {
      height: 100px;
      line-height: 100px;
    }
  }
}
.usercomment-top span {
  margin-bottom: 50px;
  font-weight: 800;
}
/* 用户评论結束 */
</style>
