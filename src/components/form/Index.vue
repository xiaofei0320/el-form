<template>
    <div>
        <KForm :model="model" :rules="rules" ref="loginForm">
            <KFormItem label="用户名" prop="username">
                <KInput v-model="model.username" placeholder="请输入用户名"></KInput>
            </KFormItem>
            <KFormItem label="密码" prop="password">
                <KInput v-model="model.password" placeholder="请输入密码"></KInput>
            </KFormItem>
            <KFormItem>
                <button @click="onClick">登录</button>
            </KFormItem>
        </KForm>
    </div>
</template>

<script>
    import KInput from '@/components/form/KInput.vue'
    import KFormItem from '@/components/form/KFormItem.vue'
    import KForm from '@/components/form/KForm.vue'
    import Notice from '@/components/Notice.vue'
    export default {
        components: {
            KInput,
            KFormItem,
            KForm
        },
        data() {
            return {
                rules: {
                    username: [{ required: true, message: "请输⼊⽤户名" }],
                    password: [{ required: true, message: "请输⼊密码" }]
                },
                model: {
                    username: '',
                    password: ''
                }
            };
        },
        methods: {
            onClick() {
                this.$refs.loginForm.validate(isValid => {
                    if(isValid) {
                        this.$create(Notice, {
                           title: '校验成功',
                       }).show()
                    } else {
                       this.$create(Notice, {
                           title: '校验失败',
                           message: '校验错误请重试'
                       }).show()
                    }
                })
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>