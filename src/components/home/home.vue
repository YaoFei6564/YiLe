<template>
  <div class="content">
    <Card style="border:none;margin: 16px 0;">
      <div class="ivu-page-header-title">系统首页</div>
    </Card>
    <Card :style="{margin: '16px 20px', background: '#fff',height:'auto'}">
      <p slot="title">
        待处理事务
      </p>
      <Row>
        <Col span="8" style="height: 35px;padding: 0 20px" v-for="(item,index) in statusList" :key="index">
          <a @click="order(item.Id)">{{item.Name}}</a> ({{orderNum["num"+String(index+1)]}})
        </Col>
      </Row>

    </Card>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        statusList:[],
        orderNum:{}
      }
    },
    methods: {
      //获取状态
      getStatus() {
        const _this = this;
        _this.Axios.get('/Manage/Order/getStateStr').then(res => {
          _this.statusList = res.data.data;
        })
      },

      //根据ID 跳转到订单页面
      order(Id){
        this.menu1 = '3';
        this.$emit('operateMuen','3','3-1-1');
        this.$router.push({
          name:'订单列表',
          params:{
            id:Id
          }
        });
      },

      //获取状态数量
      getOrderNum(){
        const _this = this;
        _this.Axios.get('/Manage/Order/getOrderNum').then(res => {
          _this.orderNum=res.data;
        });
      },
    },
    mounted() {
      this.getStatus();
      this.getOrderNum()

    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  .shiwu{
    float: left;
    margin-right: 4px;
    margin-top:2px;
    width: 16px
  }
</style>
