<template>
    <div>
        <i-form :model="checkForm" :rules="checkFormRules">
            <i-form-item label="用户名" prop="name">
                <i-input v-model="checkForm.name"></i-input>
            </i-form-item>
            <i-form-item label="邮箱" prop="mail">
                <i-input v-model="checkForm.mail"></i-input>
            </i-form-item>
            <button>提交</button>
            <button>重置</button>
        </i-form>
    </div>
</template>
<script>
import iForm from '../components/form/form'
import iFormItem from '../components/form/form-item'
import iInput from '../components/input/input'
export default {
    components: {
        iForm,
        iFormItem,
        iInput
    },
    data () {
        return {
            checkForm: {
                name: '',
                mail: ''
            },
            checkFormRules: {
                name: [
                    { required: true, message: '用户名不能为空', trigger: 'blur' }
                ],
                mail: [
                    { required: true, message: '邮箱不能为空', trigger: 'blur' },
                    { type: 'email', message: '邮箱格式不正确', trigger: 'blur' }
                ],
            }
        }
    }
}
</script>
<style lang="less" scoped>

</style>