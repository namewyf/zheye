<template>
  <div class="create-post-page">
    <h4>新建文章</h4>
    <validate-form @form-submit="onFormSubmit">
    <div class="mb-3">
        <label class="form-label">文章标题：</label>
        <validate-input
        :rules="titleRules" v-model="titleVal"
        placeholder="请输入文章标题"
        type="text"
        >
    </validate-input>
    </div>
    <div class="mb-3">
        <label class="form-label">文章详情：</label>
        <validate-input
        rows="10"
        type="text"
        tag="textarea"
        placeholder="请输入文章详情"
        :rules="contentRules"
        v-model="contentVal"
       >
        </validate-input>
        <template>
            <button class="btn btn-primary btn-large">发表文章</button>
        </template>
    </div>
</validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { GlobalDataProps } from '../store'
import { PostProps } from '@/testData'
import ValidateInput, { RulesProp } from '../components/ValidateInput.vue'
import ValidateForm from '../components/ValidateForm.vue'
export default defineComponent({
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Login',
  components: {
    ValidateInput,
    ValidateForm
  },
  setup () {
    const titleVal = ref('')
    const router = useRouter()
    const store = useStore<GlobalDataProps>()
    const titleRules: RulesProp = [
      { type: 'required', message: '文章标题不能为空' }
    ]
    const contentRules: RulesProp = [
      { type: 'required', message: '文章详情不能为空' }
    ]
    const contentVal = ref('')
    const onFormSubmit = (result:boolean) => {
      if (result) {
        const { columnId } = store.state.user
        if (columnId) {
          const newPost:PostProps = {
            id: new Date().getTime(),
            title: titleVal.value,
            content: contentVal.value,
            columnId,
            createAt: new Date().toLocaleString()
          }
          store.commit('createPost', newPost)
          router.push({ name: 'column', params: { id: columnId } })
        }
      }
    }
    return {
      titleRules,
      titleVal,
      contentRules,
      onFormSubmit,
      contentVal
    }
  }
})
</script>

<style lang="scss" scoped>

</style>
