<template>
  <div class="sign">
    <el-form
      :model="ruleForm"
      status-icon
      :rules="rules"
      ref="ruleForm"
      label-width="100px"
      class="demo-ruleForm"
    >
      <el-form-item label="账号" prop="user">
        <el-input v-model="ruleForm.user" autocomplete="off" placeholder="请输入用户名"></el-input>
      </el-form-item>

      <el-form-item label="密码" prop="pass">
        <el-input type="password" v-model="ruleForm.pass" autocomplete="off" placeholder="请输入密码"></el-input>
      </el-form-item>

      <el-form-item label="确认密码" prop="checkPass">
        <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
      </el-form-item>

      <el-form-item label="年龄" prop="age">
        <el-input v-model.number="ruleForm.age"></el-input>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>

        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "Sign",

  props: [],

  components: {},

  data() {
    var validateUser = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("用户名不能为空"));
      }
      setTimeout(() => {
        if (!value.match(/^[a-zA-Z0-9]{8,}/)) {
          return callback(new Error("用户名至少八位且包含数字、大小写"));
        } else {
          callback();
        }
      }, 500);
    };
    var checkAge = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
            callback();
          }
        }
      }, 500);
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      ruleForm: {
        user: "",
        pass: "",
        checkPass: "",
        age: ""
      },
      rules: {
        user: [
          { validator: validateUser, trigger: "blur" }
        ],
        pass: [
          { validator: validatePass, trigger: "blur" }
        ],
        checkPass: [
          { validator: validatePass2, trigger: "blur" }
        ],
        age: [
          { validator: checkAge, trigger: "blur" }
        ]
      }
    };
  },

  //方法 函数写这里

  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
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

  destroyed() {}
};
</script>


<style lang="scss" scoped>
</style>