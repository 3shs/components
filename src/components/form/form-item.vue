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
import AsyncValidator from 'async-validator'
export default {
    name: 'iFormItem',
    mixins: [ Emitter ],
    inject: ['form'],
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
    computed: {
        fieldVlalue () {
            return this.form.model[this.prop]
        }
    },
    mounted () {
        if (this.prop) {
            this.dispatch('iForm', 'on-form-item-add', this)    
            this.setRules()
        }
    },
    methods: {
        getRules () {
            let formRules = this.form.rules
            
        },
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