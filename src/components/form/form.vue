<template>
    <form>
        <slot></slot>
    </form>
</template>
<script>
export default {
    provide: {
        form: this
    },
    name: 'iForm',
    props: {
        model: {
            type: Object
        },
        rules: {
            type: Object
        }
    },
    data () {
        return {
            fields: []
        }
    },
    created () {
        this.$on('on-form-item-add', field => {
            if (field) this.fields.push(field)
        })
        this.$on('on-form-item-remove', field => {
            if (field.props) this.fields.splice(this.fields.indexOf(field), 1)
        })
    },
    methods: {
        validate (callback) {
            return new Promise( resolve => {
                this.fields.forEach( field => {
                    field.validate()
                })
            })
        }
    }
}
</script>
<style lang="less" scoped>

</style>