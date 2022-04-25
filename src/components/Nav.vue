<template>
  <div class="nav">
      <ul class="topNav">
          <li>
              <router-link to="/" target='_blank'>首页</router-link>
          </li>
          <li>
              <router-link to="/" target='_blank'>商城</router-link>
          </li>
          <li>
              <router-link to="/" target='_blank'>库存</router-link>
          </li>
      </ul>
      <div id="head">
          <div @click="user()">
              <el-avatar icon="el-icon-user-solid"></el-avatar>
          </div>

            <!-- 第一次点开是登录的模态框 -->
            <el-dialog title="登 录" :visible.sync="dialogFormVisible">
            <el-form :model="form">
                <el-form-item label="用户名" :label-width="formLabelWidth">
                    <el-input v-model="form.name" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="密码" :label-width="formLabelWidth">
                    <el-input type="password" v-model="form.pass" show-password autocomplete="off"></el-input>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="dialogFormVisible = false"><router-link to="/Sign">注 册</router-link></el-button>
                <el-button type="primary" @click="sign()">确 定</el-button>
            </div>
            </el-dialog>

            <!-- 登录成功后是菜单列表 -->
            <div id="more" v-show="more">
                <ul>
                    <li class="el-icon-info">
                        <router-link to="/about" target='_blank'>关于</router-link>
                    </li>
                    <li class="el-icon-switch-button" @click="closeSign()">注销</li>
                </ul>
            </div>
      </div>
  </div>
</template>

<script>
 

export default {
  name: 'Nav',
  props:[],
  components: {
   
  },
  data() {
    return {
        token: false,
        more: false,
        dialogFormVisible: false,
        form: {
          name: '',
          pass: '',
          type: []
        },
        formLabelWidth: '100px'
    };
  },
  //方法 函数写这里
  methods: {
    user: function(){
        if ( this.token == false) {
            this.dialogFormVisible = true;
        } else {
            this.more = true;
        }
    },
    closeSign: function(){
        this.token = false;
        this.more = false;
    },
    sign: function(){
        this.dialogFormVisible = false;
        this.token = true;
        // this.$message('这是一条消息提示');
        this.$message({
            type: 'success',
            message: '欢迎 ' + this.form.name + ' 登录'
        });
    }
  },
  //计算属性
  computed: {},
  //侦听器
  watch: {},
  //过滤器
  filters: {},
  //以下是生命周期
  //组件创建之前
  beforeCreate() {},
  //组件创建之后
  created() {},
  //页面渲染之前
  beforeMount() {},
  //页面渲染之后
  mounted() {},
  //页面视图数据更新之前
  beforeUpdate() {},
  //页面视图数据更新之后
  updated() {},
   //页面销毁之前
  beforeDestroy() {},
  //页面销毁之后
  destroyed() {},
}
</script>


<style scoped>
.router-link-active {
    text-decoration: none;
    color: #2c3e50;
}

div a {
    text-decoration: none;
    color: #2c3e50;
}

.nav {
    margin: 0;
    position: relative;
    left: 0;
    top: 0;
    width: 100%;
    height: 5rem;
    background: #000;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.topNav {
    height: 5rem;
    display: flex;
    align-items: center;
}

.topNav li {
    margin: 0 1rem;
    float: left;
    list-style: none;
}

#head {
    margin-right: 2rem;
    float: right;
    position: relative;
}

#more {
    width: 5rem;
    height: 6rem;
    background: #ccc;
    position: absolute;
    left: -1.5rem;
}

#more ul {
    height: 6rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}

#more li {
    list-style: none;
}

#more li a {
    text-decoration: none;
    color: #2c3e50;
}

#modal {
    width: 20rem;
    height: 20rem;
    background: #2c3e50;
}
</style>