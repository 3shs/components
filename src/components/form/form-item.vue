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
            formRules = formRules ? formRules[this.prop] : []
            return [].concat(formRules || [])
        },
        // 只支持blur和change事件
        getFilterRules (trigger) {
            // blur
            const rules = this.getRules()
            return rules.filter( rule => !rule.trigger || rule.trigger.indexOf(trigger) !== -1)
        },
        setRules () {
            this.$on('on-form-blur', this.onFieldBlur)
            this.$on('on-form-change', this.onFieldChange)
        },
        validate (trigger, callback = function () {}) {
            let rules = this.getFilterRules(trigger)
        },
        onFieldBlur () {
            this.validate('blur')
        },
        onFieldChange () {
            this.validate('change')
        }
    },
    beforeDestroy () {
        this.dispatch('iForm', 'on-form-item-remove', this)
    }
}
</script>
<style lang="less" scoped>

</style>