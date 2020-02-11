<template>
<div>
    <el-form ref="loginForm" :model="loginForm" :rules="loginRules" label-width="25%" auto-complete="on" label-position="right">
        <el-form-item prop="username" label="用户名">
            <el-input v-model="loginForm.username" ref="username" name="username" auto-complete="on" type="text" placeholder="请输入用户名" />
        </el-form-item>
        <el-form-item prop="password" label="密码">
            <el-input v-model="loginForm.password" ref="password" name="password" :type="passwordType" auto-complete="on" @keyup.enter.native="handleLogin" placeholder="请输入密码" />
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="handleLogin">登录</el-button>
            <el-button @click="resetForm()">重置</el-button>
        </el-form-item>
    </el-form>
</div>
</template>

<script>
export default {
    name: "Login",
    data() {
        const valid_map = ['admin', 'editor'];
        const validUsername = (rule, value, callback) => {
            if (valid_map.indexOf(value.trim()) < 0) {
                callback(new Error('请输入正确的用户名'))
            } else {
                callback()
            }
        }
        const validPassword = (rule, value, callback) => {
            if (value.length < 6) {
                callback(new Error('密码不能低于6位'))
            } else {
                callback()
            }
        }
        return {
            loginForm: {
                username: '',
                password: ''
            },
            passwordType: 'password',
            loginRules: {
                username: [{
                    required: true,
                    trigger: 'blur',
                    validator: validUsername
                }],
                password: [{
                    required: true,
                    trigger: 'blur',
                    validator: validPassword
                }]
            },
        }
    },
    methods: {
        showPwd() {
            this.passwordType === "password" ? this.passwordType === "text" : this.passwordType = "password";
        },
        handleLogin() {
            this.$refs.loginForm.validate(valid => {
                if (valid) {
                    // const loginUrl = 'http://localhost:8081/user/getUserData';
                    // this.$ajax.get(loginUrl)
                    // .then(
                    //     response => {
                    //         const rstData = response.data;
                    //         console.log(rstData);
                    //     }
                    // ).catch(
                    //     response => {
                    //         alert('请求失败');
                    //     }
                    // )
                    const loginUrl="http://localhost/user-api/loginData";
                    let formData = new FormData();
                    for(var key in this.loginForm){
                        formData.append(key,this.loginForm[key]);
                    }
                    this.$ajax.post(
                        loginUrl,
                        formData,
                        {
                            "Content-Type": "application/json;charset=utf-8"
                        }
                    ).then(
                        res => {
                            const rstData = res.data;
                            if(rstData.msg != '密码不正确'){
                                this.$message({message:rstData.msg,type: 'success'});
                                this.$router.push({path:"/second"});
                            }else{
                                this.$message.error(rstData.msg);  
                            }
                        }
                    ).catch(
                        res => {
                            this.$message.error('请求失败');
                        }
                    )
                } else {
                    return false
                }
            })
        },
        resetForm() {
            this.$refs.loginForm.resetFields();
        }
    },
}
</script>

<style>
.el-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 60px 35px 60px;
    background: #889aa4;
    margin: 0 auto;
    overflow: hidden;
}

.el-input {
    width: 65%;
    background: transparent;
    border: 0px;
    -webkit-appearance: none;
    border-radius: 0px;
    color: #fff;
    height: 47px;
    caret-color: #fff;
}

.svg-container {
    padding: 6px 5px 6px 15px;
    color: #889aa4;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
}

.show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: #889aa4;
    cursor: pointer;
    user-select: none;
}
</style>
