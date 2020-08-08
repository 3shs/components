<template>
    <div>
        <label v-if="label"> {{label}} </label>
        <div>
            <slot></slot>
        </div>
    </div>
</template>
<script>
import Emitter from '../../minxins/emitter'
export default {
    name: 'iFormItem',
    mixins: [ Emitter ],
    props: {
        label: {
            type: String,
            default: ''
        },
        prop: {
            type: String
        }
    },
    data () {
        return {

        }
    },
    mounted () {
        if (this.prop) {
            this.dispatch('iForm', 'on-form-item-add', this)
            this.setRules()
        }
    },
    methods: {
        setRules () {
            this.$on('on-form-blur', this.onFieldBlur)
            this.$on('on-form-change', this.onFieldChange)
        },
        onFieldBlur () {

        },
        onFieldChange () {

        }
    },
    beforeDestroy () {
        this.dispatch('iForm', 'on-form-item-remove', this)
    }
}
</script>
<style lang="less" scoped>

</style>