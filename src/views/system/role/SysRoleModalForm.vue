<template>
  <a-modal
    :title="title"
    :visible="visible"
    :mask-closable="false"
    :body-style="{paddingBottom: '8px'}"
    :confirm-loading="submitLoading"
    @ok="handleSubmit"
    @cancel="handleClose"
  >
    <a-form
      :form="form"
      :label-col="labelCol"
      :wrapper-col="wrapperCol"
    >
      <a-form-item
        v-if="isUpdateForm"
        style="display: none"
      >
        <a-input v-decorator="['id']" />
      </a-form-item>

      <a-form-item label="角色名">
        <a-input
          v-decorator="['name', decoratorOptions.name]"
          placeholder="角色名"
        />
      </a-form-item>

      <a-form-item label="角色标识">
        <a-input
          v-decorator="['code', decoratorOptions.code]"
          :disabled="isUpdateForm"
          placeholder="角色标识必须以ROLE_开头!"
        />
      </a-form-item>

      <a-form-item label="角色类型">
        <a-radio-group
          v-decorator="['type', decoratorOptions.type]"
          :disabled="isUpdateForm"
        >
          <a-radio-button :value="1">
            系统角色
          </a-radio-button>
          <a-radio-button :value="2">
            业务角色
          </a-radio-button>
        </a-radio-group>
      </a-form-item>

      <a-form-item label="备注">
        <a-textarea
          v-decorator="['note']"
          :auto-size="{ minRows: 4, maxRows: 8 }"
          placeholder="备注信息"
        />
      </a-form-item>
    </a-form>
  </a-modal>
</template>

<script>
import { PopUpFormMixin } from '@/mixins'
import { addObj, putObj } from '@/api/system/role'

export default {
  name: 'RoleModalForm',
  mixins: [PopUpFormMixin],
  data () {
    return {
      reqFunctions: {
        create: addObj,
        update: putObj
      },

      labelCol: {
        sm: { span: 24 },
        md: { span: 5 }
      },
      wrapperCol: {
        sm: { span: 24 },
        md: { span: 19 }
      },

      decoratorOptions: {
        name: {
          rules: [{ required: true, message: '请输入角色名!' }]
        },
        code: {
          rules: [{ required: true, message: '请输入角色标识!' }
            , { validator: this.validateCode }
          ]
        },
        type: {
          initialValue: 1
        }
      }
    }
  },
  methods: {
    validateCode (rule, value, callback) {
      if (value && value.indexOf('ROLE_') !== 0) {
        callback('角色标识必须以ROLE_开头！')
      }
      callback()
    }
  }
}
</script>


