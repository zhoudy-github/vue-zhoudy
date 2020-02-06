<!--<template>
   <div class='first'>
       {{msg}}
       <Confirm text='注册' @message='getMessage'></Confirm>
       <p><router-link to='/second'>子页面</router-link></p>
   </div>
</template>

<script>
import Confirm from '@/components/sub/Confirm'
export default {
    name: 'First',
    components: {
        Confirm
    },
    data(){
        return {
            msg: 'Hello Vue'
        }
    },
    methods: {
        getMessage(val){
            alert(val);
        }
    }
}
</script>
<style lang='less' scope>
    .first {
        color: blue;
        font-size: 30px;
    }
</style>-->