<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <router-view></router-view>
    <footer class="text-center py-4 text-secondary bg-light mt-6">
      <small>
        <ul class="list-inline mb-0">
          <li class="list-inline-item">@ 2020 者也专栏</li>
          <li class="list-inline-item">课程</li>
          <li class="list-inline-item">文档</li>
          <li class="list-inline-item">联系</li>
          <li class="list-inline-item">更多</li>
        </ul>
      </small>
    </footer>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from '@/components/ColumnList.vue'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from '@/components/ValidateInput.vue'
import ValidateForm from '@/components/ValidateForm.vue'
import ColumnDetail from '@/views/ColumnDetail.vue'

const currentUser: UserProps = {
  isLogin: true,
  name: 'yuwei'
}
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: 'test1的专栏，有一段非常有意思的简介',
    avatar: 'https://cn.vuejs.org/images/logo.png'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: 'test2的专栏，有一段非常有意思的简介',
    avatar: 'https://cn.vuejs.org/images/logo.png'
  },
  {
    id: 3,
    title: 'test3的专栏',
    description: 'test2的专栏，有一段非常有意思的简介'
    // avatar: 'https://cn.vuejs.org/images/logo.png'
  },
  {
    id: 4,
    title: 'test4的专栏',
    description: 'test2的专栏，有一段非常有意思的简介',
    avatar: 'https://cn.vuejs.org/images/logo.png'
  }
]
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader
  },
  setup () {
    const inputRef = ref<any>()
    const emailVal = ref('yuwei')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = ' can not be empty'
      }
    }
    const onFormSubmit = (result: boolean) => {
      console.log('result', inputRef.value.validateInput())
    }
    return {
      list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      onFormSubmit,
      inputRef
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
