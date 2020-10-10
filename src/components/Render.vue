<template>
  <el-form-item
    :label="element.label"
    label-width="100px"
    :class="model === 'custom' ? 'custom-item' : ''"
    :required="element.required"
  >
    <!-- 下拉框 -->
    <el-select
      v-if="element.type === 'select'"
      v-model="element.value"
      :placeholder="element.placeholder || '请选择'"
      :maxLength="element.maxLength"
      :clearable="element.clearable"
    >
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      ></el-option>
    </el-select>
    <!-- 单行文本框 -->
    <el-input
      v-if="element.type === 'input'"
      v-model="element.value"
      :placeholder="element.placeholder || '请输入内容'"
      :maxLength="element.maxLength"
      :clearable="element.clearable"
    ></el-input>
    <!-- 多行文本框 -->
    <el-input
      v-if="element.type === 'textarea'"
      type="textarea"
      :rows="2"
      v-model="element.value"
      :placeholder="element.placeholder || '请输入内容'"
      :maxLength="element.maxLength"
      :clearable="element.clearable"
    ></el-input>
	
    <!-- 日期选择器 -->
    <el-date-picker
      v-if="element.type === 'datePicker'"
      v-model="element.value"
      type="date"
      :placeholder="element.placeholder || '请选择日期'"
      :maxLength="element.maxLength"
      :clearable="element.clearable"
    ></el-date-picker>
		
	<!-- 性别选择器 -->
	<el-radio
	v-if="element.type === 'radio'"
	v-model="element.value"
	label="1"
	>
	男
	</el-radio>
	<el-radio
	v-if="element.type === 'radio'"
	v-model="element.value"
	label="2"
	>
	女
	</el-radio>
	
	<!-- 计数器 -->
	<el-input-number
	v-if="element.type === 'number'"
	v-model="element.value"
	@change="handleChange"
	:min="1"
	:max="10"
	label="计数器"
	></el-input-number>
	
	
	
    <!-- 按钮组 -->
    <section class="btn-group" v-if="model === 'custom'">
      <el-button
        type="primary"
        icon="el-icon-edit"
        plain
        circle
        size="mini"
        :class="
          element.dictionary === '' || !element.dictionary
            ? 'warn-btn edit-btn'
            : 'edit-btn'
        "
        :title="
          element.dictionary === '' || !element.dictionary
            ? '请填写唯一标识，否则无效'
            : '编辑'
        "
        @click="editElement(element)"
      ></el-button>
      <el-button
        type="danger"
        icon="el-icon-delete"
        plain
        circle
        title="删除"
        size="mini"
        @click="deleteElement(element)"
      ></el-button>
    </section>
  </el-form-item>
</template>

<script>
export default {
  name: "renders",
  props: {
    element: Object,
    model: String,
  },
  data() {
    return {
      options: [
        { label: "数据1", value: 1 },
        { label: "数据2", value: 2 },
        { label: "数据3", value: 3 },
        { label: "数据4", value: 4 },
      ],
    };
  },
  methods: {
    editElement(ele) {
      this.$emit("editElement", ele);
    },
    deleteElement(ele) {
      this.$emit("deleteElement", ele);
    },
	handleChange(value){
		console.log(value);
	},
  },
  computed: {
    // itemClass() {
    //   let className = "";
    //   if (this.model === "custom") {
    //     if (this.element.dictionary === "" || !element.dictionary) {
    //       className = "custom enable";
    //     } else {
    //       className = "custom";
    //     }
    //   }
    //   return className;
    // }
  },
};
</script>
<style scoped>
.btn-group {
  display: inline-block;
  vertical-align: top;
  margin-left: 10px;
}
.edit-btn {
  position: relative;
}
.warn-btn::after {
  content: "!";
  display: block;
  position: absolute;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  color: #fff;
  text-align: center;
  line-height: 12px;
  font-size: 12px;
  background-color: #f56c6c;
  border: 1px solid #fff;
  top: -2px;
  right: -7px;
}
.custom-item >>> .el-form-item__content > div {
  max-width: 80%;
}
</style>