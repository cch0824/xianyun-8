<template>
  <div class="stayInfo">
    <el-form :model="form" class="stayInfo-search">
      <el-form-item>
        <!-- fetch-suggestions 返回输入建议的方法 -->
        <!-- select 点击选中建议项时触发 -->
        <!-- elementUI input 下拉列表 -->
        <el-autocomplete
          :fetch-suggestions="queryCitySearch"
          placeholder="目的地"
          @select="handleCitySelect"
          class="el-autocomplete"
          v-model="form.city"
        ></el-autocomplete>
      </el-form-item>
      <el-form-item>
        <el-date-picker
          v-model="form.time"
          type="datetimerange"
          range-separator="-"
          start-placeholder="入住日期"
          end-placeholder="离店日期"
        ></el-date-picker>
      </el-form-item>
      <el-form-item>
        <el-popover
          placement="bottom"
          width="350"
          trigger="click"
          content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。"
        >
          <el-row
            type="flex"
            justify="space-between"
            style="padding-bottom:20px;border-bottom:1px solid #eee"
          >
            <el-col :span="8" class="roomCount">
              <span>每间</span>
            </el-col>
            <el-col :span="16">

              <el-select
                v-model="form.adult"
                placeholder="成人"
                size="mini"
                style="width:100px"
                @change="handleAdult"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                ></el-option>
              </el-select>

              <el-select
                v-model="form.children"
                placeholder="儿童"
                size="mini"
                style="width:100px"
                @change="handleChildren"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                ></el-option>
              </el-select>
            </el-col>
          </el-row>
          <el-row type="flex" justify="end" style="margin-top:10px">
            <el-button type="primary" size="mini" @click="confirmUsers">确定</el-button>
          </el-row>
          <el-input slot="reference" v-model="stayUsers" placeholder="人数未定" suffix-icon="el-icon-s-custom"></el-input>
        </el-popover>
      </el-form-item>
      <el-button type="primary" style="height:40px">查看价格</el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value1: "",
      value2: "",
      cityData: [],
      form: {
        city: "",
        time: "",
        adult: "",
        children: ""
      },
      // 房间人数
      options: [
        {
          value: "1",
          label: "1"
        },
        {
          value: "2",
          label: "2"
        },
        {
          value: "3",
          label: "3"
        },
        {
          value: "4",
          label: "4"
        },
        {
          value: "5",
          label: "5"
        },
        {
          value: "6",
          label: "6"
        },
        {
          value: "7",
          label: "7"
        }
      ],
      // 最终住房人数
      stayUsers: ""
    };
  },
  methods: {
    // 确定最终人数
    confirmUsers() {
      this.stayUsers = this.form.adult + " " + this.form.children;
    },
    // 成人人数
    handleAdult(val) {
      this.form.adult = `${val} 成人`;
    },
    // 儿童人数
    handleChildren(val) {
      this.form.children = `${val} 儿童`;
    },
    // 城市搜索框发生变化时调用,获取焦点时触发
    queryCitySearch(value, cb) {
      if (!value) {
        cb([]);
        return;
      }

      this.$axios({
        url: "/cities",
        params: {
          name: value
        }
      }).then(res => {
        console.log(res);
        let arr = [];
        res.data.data.forEach(item => {
          arr.push({ value: item.name });
        });
        cb(arr);
      });
    },
    // 点击选中建议项时触发 返回选中建议值
    handleCitySelect(val) {
        // console.log(val,555)
      this.form.city = val.value;
      console.log(this.form)
    },
    showUserInfo() {
      console.log(123);
    },
    hiddenUserInfo() {
      console.log(520);
    }
  }
};
</script>
<style lang="less" scoped>
.stayInfo {
  .stayInfo-search {
    display: flex;
    div {
      margin-right: 5px;
    }
  }
}

.roomCount {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
</style>
