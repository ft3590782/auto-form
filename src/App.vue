<template>
  <div id="app">
    <auto-form v-model="formData" :show-footer="false" :span="24"></auto-form>
    <el-button type="primary" @click="submit()">确 定</el-button>

    <div>
      <textarea rows="10" name="" id="submitResult"></textarea>

      <el-button type="primary" @click="recover()">从数据恢复</el-button>
    </div>
  </div>
</template>

<script>
import {
  autoFormDataToPostData,
  dataToAutoFormData,
  // dataToAutoFormData,
} from "@/components/AutoForm/autoFormHelper";
import AutoForm from "@/components/AutoForm";
import { isEmail } from "@/components/AutoForm/formValidatorHelper";
export default {
  name: "App",
  components: {
    AutoForm,
  },
  data() {
    return {
      formData: {
        name: {
          code: "name",
          apiCode: "nameData",
          title: "姓名",
          value: "",
          type: "text",
        },
        email: {
          code: "email",
          apiCode: "emailData",
          title: "email",
          value: "",
          type: "text",
          rules: [isEmail()],
        },
        grader: {
          code: "grader",
          apiCode: "graderData",
          title: "性别",
          value: "",
          type: "select",
          options: [
            { value: 0, label: "男" },
            { value: 1, label: "女" },
          ],
        },
        age: {
          code: "age",
          apiCode: "ageData",
          title: "年龄",
          value: "",
          type: "number",
        },
        hobby: {
          code: "hobby",
          apiCode: "hobbyData",
          title: "兴趣",
          value: "",
          type: "radiogroup",
          options: [
            { value: "swimming", label: "游泳" },
            { value: "reading", label: "阅读" },
            { value: "running", label: "跑步" },
          ],
        },
        location: {
          code: "location",
          apiCode: "locationData",
          title: "位置",
          value: "",
          type: "cascader",
          props: {
            multiple: true,
          },
          options: [
            {
              value: 1,
              label: "东南",
              children: [
                {
                  value: 2,
                  label: "上海",
                  children: [
                    { value: 3, label: "普陀" },
                    { value: 4, label: "黄埔" },
                    { value: 5, label: "徐汇" },
                  ],
                },
                {
                  value: 7,
                  label: "江苏",
                  children: [
                    { value: 8, label: "南京" },
                    { value: 9, label: "苏州" },
                    { value: 10, label: "无锡" },
                  ],
                },
                {
                  value: 12,
                  label: "浙江",
                  children: [
                    { value: 13, label: "杭州" },
                    { value: 14, label: "宁波" },
                    { value: 15, label: "嘉兴" },
                  ],
                },
              ],
            },
            {
              value: 17,
              label: "西北",
              children: [
                {
                  value: 18,
                  label: "陕西",
                  children: [
                    { value: 19, label: "西安" },
                    { value: 20, label: "延安" },
                  ],
                },
                {
                  value: 21,
                  label: "新疆维吾尔族自治区",
                  children: [
                    { value: 22, label: "乌鲁木齐" },
                    { value: 23, label: "克拉玛依" },
                  ],
                },
              ],
            },
          ],
        },
      },
    };
  },
  methods: {
    submit() {
      console.log(this.formData);
      const postData = { ...autoFormDataToPostData(this.formData) };
      console.log("get submit", postData);
      // console.log("formData", this.formData);
      // console.log("postData", postData);
      // console.log("autoFormData", dataToAutoFormData(postData));
      document.getElementById("submitResult").value = JSON.stringify(postData);
    },
    recover() {
      const val = document.getElementById("submitResult").value;
      console.log(val);
      if (val !== "") {
        const value = JSON.parse(val);
        const recoverData = dataToAutoFormData(value, this.formData);
        console.log(recoverData);
        this.formData = recoverData;
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  width: 100vw;
  height: 100vh;
}
</style>
