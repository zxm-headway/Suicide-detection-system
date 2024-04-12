<!-- 用户管理 -->
<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-col :span="14">
        <el-card title="请输入文本或上传文件" style="max-width: 100%">
          <div class="text-input-component">
            <el-input
              type="textarea"
              v-model="textInput"
              placeholder="请输入文本或上传文件"
              rows="4"
            />

            <el-upload
              class="upload-demo"
              action="https://jsonplaceholder.typicode.com/posts/"
              :http-request="handleUpload"
              :before-upload="beforeUpload"
              :on-success="handleSuccess"
              :on-error="handleError"
            >
              <template #trigger>
                <el-button size="small" type="primary">点击上传文件</el-button>
              </template>
              <template #tip>
                <div class="el-upload__tip">只支持 txt 文件</div>
              </template>
            </el-upload>

            <el-button type="success" @click="openDialog">分析</el-button>

            <!-- 风险等级对话框 -->
          </div>
        </el-card>
      </el-col>
      <el-col :span="10">
        <el-card style="max-width: 100%">
          <p v-for="o in 4" :key="o" class="text item">
            {{ "List item " + o }}
          </p>
        </el-card>
      </el-col>
    </el-row>
  </div>

  <el-dialog title="风险等级" v-model="dialogVisible" width="30%">
    <div>无风险</div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">确定</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup lang="ts">
defineOptions({
  name: "User",
  inheritAttrs: false,
});
const textInput = ref("");
const dialogVisible = ref(false);
const handleUpload = (file: any) => {
  return new Promise((resolve) => {
    const reader = new FileReader();
    reader.onload = (e: any) => {
      textInput.value = e.target.result;
      // resolve();
    };
    reader.readAsText(file.file);
  });
};

const beforeUpload = (file: any) => {
  const isTxt = file.type === "text/plain";
  if (!isTxt) {
    ElMessage.error("只能上传 txt 文件");
  }
  return isTxt;
};

const handleSuccess = () => {
  ElMessage.success("文件上传成功");
};

const handleError = () => {
  ElMessage.error("文件上传失败");
};

const analyzeContent = () => {
  console.log("分析内容：", textInput.value);
  // 这里可以添加分析内容的逻辑
};

const openDialog = () => {
  dialogVisible.value = true; // 打开对话框
  console.log("打开对话框");
};
</script>

<style lang="scss" scoped>
.text-input-component {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 20px; /* 控制按钮之间的间距 */
  margin-top: 20px; /* 上边距 */
}

.upload-demo .el-upload__tip {
  margin-top: 1rem;
  font-size: 12px;
  color: #999;
}
</style>
