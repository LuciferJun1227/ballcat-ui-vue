<template>
  <a-radio-group
    :disabled="disabled"
    :value="selectedValue"
    @change="handleChange"
  >
    <a-radio v-for="dict in dictItems" :key="dict.id" :value="getValByItem(dict)">
      {{ dict.name }}
    </a-radio>
  </a-radio-group>
</template>
<script>
import DictMixin from '@/components/Dict/dictMixin'
import dictItemMixin from '@/components/Dict/dictItemMixin'

export default {
  name: 'DictRadioGroup',
  mixins: [DictMixin, dictItemMixin]
}
</script>
