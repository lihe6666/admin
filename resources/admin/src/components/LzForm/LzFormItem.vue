<script>
import { Form } from 'ant-design-vue'

export default {
  name: 'LzFormItem',
  extends: Form.Item,
  provide() {
    return {
      lzFormItem: this,
    }
  },
  props: {
    /**
     * 以 tooltip 的形式展示提示文字
     */
    tip: String,
    /**
     * 表单中的 name 值
     */
    prop: String,
    /**
     * 编辑模式下必填，会在 LzForm 中，自动修改 required 为 true
     */
    requiredWhenEdit: Boolean,
    /**
     * 添加模式下必填
     */
    requiredWhenCreate: Boolean,
  },
  methods: {
    renderLabel() {
      const vnode = Form.Item.methods.renderLabel.bind(this)(...arguments)
      if (vnode && this.tip) {
        vnode.componentOptions.children.push((
          <a-tooltip placement="topLeft" class="ml-1">
            <span slot="title" domPropsInnerHTML={this.tip.replace(/\n/g, '<br>')}/>
            <a-icon type="question-circle"/>
          </a-tooltip>
        ))
      }
      return vnode
    },
  },
}
</script>

<style scoped lang="less">
@import "~@/styles/vars";

.ant-form-item-label {
  &::after {
    content: '';
    position: relative;
    top: -0.5px;
    margin: 0 8px 0 2px;
  }

  .anticon {
    color: @primary-color;
  }
}

.ant-form-item-label > label::after {
  content: '';
  margin: 0;
}
</style>
