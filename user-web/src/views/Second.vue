<template>
    <div>
        <p>{{content}}</p>
        <a href='#/first'>返回第一个页面</a>
    </div>
</template>

<script>
export default {
    name: 'Second',
    data() {
        return {
            content : '欢迎来到第二个页面'
        }
    }
}
</script>