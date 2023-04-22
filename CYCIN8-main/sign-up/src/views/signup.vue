<template>
 <div class="wrap">
   <div class="home">
    <div class="title">Create Your Account</div>

    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      class="demo-ruleForm"
    >
      <div class="name">
        <el-form-item prop="FirstName">
          <el-input
            placeholder="First Name"
            v-model="ruleForm.FirstName"
          ></el-input>
        </el-form-item>
        <el-form-item prop="FamilyName">
          <el-input
            placeholder="Family Name"
            v-model="ruleForm.FamilyName"
          ></el-input>
        </el-form-item>
      </div>
      <el-form-item prop="EmailAddress">
        <el-input
          placeholder="Email Address"
          v-model="ruleForm.EmailAddress"
        ></el-input>
      </el-form-item>
      <el-form-item prop="Password">
        <el-input
          maxlength="15"
          placeholder="Password"
          v-model="ruleForm.Password"
        ></el-input>
      </el-form-item>

      <el-form-item>
        <el-button class="btns" type="primary" @click="submitForm('ruleForm')"
          >Sign-up</el-button
        >
      </el-form-item>
    </el-form>
  </div>
 </div>
</template>




<script>
export default {
  name: "HomeView",
  data() {
    var EmailAddress = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("Email Address"));
      } else if (!/^[a-zA-Z0-9]+([-_.][A-Za-zd]+)*@([a-zA-Z0-9]+[-.])+[A-Za-zd]{2,5}$/g.test(value)) {
        return callback(new Error("Incorrect mailbox format"));
      }  else {
        callback();
      }
    };
    return {
      ruleForm: {
        FirstName: "",
        FamilyName: "",
        EmailAddress: "",
        Password: "",
      },
      rules: {
        FirstName: [{ required: true, message: "First Name", trigger: "blur" }],
        FamilyName: [
          { required: true, message: "Family Name", trigger: "blur" },
        ],
        EmailAddress: [
          { required: true, validator: EmailAddress, trigger: "blur" },
          // { required: true, message: "Email Address", trigger: "blur" },
        ],
        Password: [{ required: true, message: "Password", trigger: "blur" }],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
  },
};
</script>

<style  scoped>
.wrap{
  width: 100vw;
  height: 100vh;
  background: url('../assets/bg.jpg') no-repeat;
  background-size: cover;
  position: relative;

}

.home {
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -200px 0 0 -255px;
  width: 440px;
  background: rgba(225,225,225,0.2);
  box-shadow: 0px 0px 8px #dfdddd;
  padding: 30px;
  border-radius: 5px;
}
.title {
  padding: 30px 0;
  font-size: 22px;
  font-weight: bold;
  text-align: center;
  color: #fff;
}
.name {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.btns {
  width: 100%;
  display: block;
  margin: 0 auto;
}
</style>

