<template>
  <div class="container">
    <a-modal v-model:visible="visible" :width="1200" draggable :footer="false" @close="resetFields">
      <template #title>
        {{ formData?.id ? '编辑域名' : '新增域名' }}
      </template>
      <a-form ref="formRef" layout="vertical" :model="formData">
        <a-space direction="vertical" :size="16">
          <a-card class="general-card">
            <template #title> 必填信息 </template>
            <a-row :gutter="80">
              <a-col :span="8">
                <a-form-item label="二维码备注" field="domainNotes" validate-trigger="input" required>
                  <a-input v-model="formData.domainNotes" placeholder="请输入" allow-clear></a-input>
                </a-form-item>
              </a-col>
              <a-col :span="8">
                <a-form-item label="域名值" field="domainValue" validate-trigger="input" required>
                  <a-input v-model="formData.domainValue" placeholder="请输入" allow-clear></a-input>
                </a-form-item>
              </a-col>
              <a-col :span="8">
                <a-form-item label="使用场景" field="scene" required>
                  <a-select v-model="formData.scene" placeholder="请选择" allow-clear>
                    <a-option :value="0">登录二维码域名</a-option>
                    <a-option :value="1">优惠券二维码域名</a-option>
                    <a-option :value="2">通道码域名</a-option>
                    <a-option :value="3">充电域名</a-option>
                  </a-select>
                </a-form-item>
              </a-col>
            </a-row>
          </a-card>
        </a-space>
        <div class="actions">
          <a-space>
            <a-button @click="resetFields"> 重置 </a-button>
            <a-button type="primary" :loading="loading" @click="onSubmitClick">
              保存
            </a-button>
          </a-space>
        </div>
      </a-form>
    </a-modal>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import { addDomain, updateDomain } from '@/api/user';
import { Message } from '@arco-design/web-vue';

const visible = ref(false);
const loading = ref(false);
const formRef = ref();
const emit = defineEmits(['fetchData', 'fetch-data']);
const formData = ref({
  "domainNotes": "",
  "domainValue": "",
  "scene": "",
  id: '',
});
const handleClick = (e: any = null) => {
  if (e?.id) {
    const newInfo = JSON.parse(JSON.stringify(e));
    formData.value = newInfo;
  }
  visible.value = true;
};
const resetFields = () => {
  formData.value.id = '';
  formRef.value.resetFields();
};
const onSubmitClick = () => {
  // eslint-disable-next-line consistent-return
  formRef.value.validate(async (valid: any) => {
    if (valid) return false;
    // @ts-ignore
    if (formData.value.id) {
      const { code } = await updateDomain(formData.value);
      if (code === 10002) {
        formRef.value.resetFields();
        visible.value = false;
        Message.success('更新成功!');
        emit('fetchData');
      }
    } else {
      const { code } = await addDomain(formData.value);
      if (code === 10002) {
        formRef.value.resetFields();
        visible.value = false;
        Message.success('添加成功!');
        emit('fetchData');
      }
    }
  });
};

defineExpose({ handleClick });
</script>

<style scoped lang="less">
.container {
  padding: 0 20px 40px 20px;
  overflow: hidden;
}

.actions {
  height: 60px;
  padding: 14px 20px 14px 0;
  background: var(--color-bg-2);
  text-align: right;
}
</style>
