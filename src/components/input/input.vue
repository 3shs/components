<template>
    <input 
        type="text"
        :value="currentValue"
        @blur="handleBlur"
        @input="handleInput" />
</template>
<script>
import Emitter from '../../minxins/emitter'
export default {
    name: 'iInput',
    mixins: [ Emitter ],
    props: {
        value: {
            type: String,
            default: ''
        }
    },
    data () {
        return {
            currentValue: this.value
        }
    },
    watch: {
        value (val) {
            this.currentValue = val
        }
    },
    methods: {
        handleBlur () {

        },
        handleInput (e) {
            const value = e.target.value
            this.currentValue = value
            // 给父组件传值 修改父组件 v-model(语法糖 其实利用的就是 input 事件) 绑定的值
            this.$emit('input', value)
            this.dispatch('iFormItem', 'on-form-change', value)
            
        },
        handleBlur () {
            this.dispatch('iFormItem', 'on-form-blur', this.currentValue)
        }
    }
}
</script>
<style lang="less" scoped>

</style>