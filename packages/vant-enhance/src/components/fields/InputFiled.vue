<script setup lang="ts">
import { type Ref } from 'vue'

import { useVModel } from '@vueuse/core'
import type { FieldEmits } from './types'
import type { FieldProps } from '@/shared/types'

defineOptions({ name: 'VeInputField' })

const props = withDefaults(defineProps<FieldProps>(), {
  readonly: false,
  disabled: false,
  rules: () => [],
  placeholder: '',
  isLink: false,
  align: 'left',
})
const emit = defineEmits<FieldEmits>()

const _value = useVModel(props, 'value', emit) as Ref<string | number>

const handleFieldClick = () => {
  if (props.readonly || props.disabled) return
  emit('click')
}
</script>

<template>
  <van-cell-group>
    <van-field
      :label="label"
      :name="name"
      v-model="_value"
      :readonly="readonly"
      :disabled="disabled"
      :placeholder="placeholder || '请输入'"
      :is-link="isLink"
      :rules="rules"
      :input-align="align"
      :type="inputType"
      :rows="inputRows"
      :maxlength="inputMaxLength"
      autosize
      show-word-limit
      @click="handleFieldClick"
    >
    </van-field>
  </van-cell-group>
</template>

<style scoped></style>
