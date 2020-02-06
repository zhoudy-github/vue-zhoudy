<template>
    <div class="confirm-button">
        <button @click="getButtonClick">{{text || '确认'}}</button>
    </div>
</template>

<script>
export default {
    name: 'Confirm',
    props: ['text'],
    data() {
        return {
            msg :'哈哈哈'
        };
    },
    methods: {
        getButtonClick() {
            this.$emit("message",this.msg);
        }
    }
}
</script>

<style>
	.confirm-button {
        margin-top: 100px;
	}
    .confirm-button button{
        width: 180px;
        height: 40px;
        font-size: 22px;
        background-color: aqua;
        outline: 0;
        border: 0;
        color: #fff;
        border-radius: 8px;
    }
</style>
