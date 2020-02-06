<template>
<div>
    <label>用户名</label>
    <input id="userName" type="text" />
    <label>密码</label>
    <input id="prd" type="password" />
    <button @click="login">确定</button>
</div>
</template>

<script>
import $ from 'jquery';
import axios from 'axios';

export default {
    name: 'Login',
    data() {
        return {}
    },
    methods: {
        login() {
            const userName = $('#userName').val();
            const loginUrl = 'http://localhost:8080/user/getUserData';
            axios.get(loginUrl).then(
                response => {
                    const rstData = response.data;
                    console.log(rstData);
                }
            ).catch(
                response => {
                    alert('请求失败');
                }
            )
        }
    }
}
</script>
