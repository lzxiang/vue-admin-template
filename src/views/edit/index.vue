<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="80px">


      <el-form-item label="标题"
        ><el-input v-model="input" placeholder="标题"
      /></el-form-item>

      <el-form-item label="摘要">
        <el-input type="textarea" v-model="form.desc"></el-input>
      </el-form-item>

      <el-form-item label="正文"><mavon-editor v-model="value" /></el-form-item>

      <el-form-item label="封面">
        <el-upload
          action="https://jsonplaceholder.typicode.com/posts/"
          list-type="picture-card"
          :on-preview="handlePictureCardPreview"
          :on-remove="handleRemove"
        >
          <i class="el-icon-plus"></i>
        </el-upload>
        <el-dialog :visible.sync="dialogVisible">
          <img width="100%" :src="dialogImageUrl" alt="" />
        </el-dialog>
      </el-form-item>

      <el-form-item label="分类">
        <el-select v-model="form.region" placeholder="请选择文章分类">
          <el-option label="分类一" value="shanghai"></el-option>
          <el-option label="分类二" value="beijing"></el-option>
        </el-select>
      </el-form-item>

      <el-form-item label="置顶">
        <el-switch v-model="form.delivery"></el-switch>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">发布</el-button>
        <el-button type="info" @click="onSubmit">草稿</el-button>
        <el-button>取消</el-button>
      </el-form-item>

    </el-form>

  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  data() {
    return {
      input: "",
      value: "",
      dialogImageUrl: "",
      dialogVisible: false,
      form: {
        name: "",
        region: "",
        delivery: false,
        type: [],
        desc: "",
      },
    };
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    handlePictureCardPreview(file) {
      this.dialogImageUrl = file.url;
      this.dialogVisible = true;
    },
    onSubmit() {
      console.log("submit!");
    },
  },
  computed: {
    ...mapGetters(["name"]),
  },
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}

</style>
