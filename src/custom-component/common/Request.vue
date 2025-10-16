<template>
  <el-collapse-item title="数据源相关" name="request" class="request-container">
    <el-form>
      <el-form-item label="表单项（如请求地址）">
        <el-input v-model.trim="request.url" @blur="validateURL">
          <template slot="prepend">HTTPS://</template>
        </el-input>
      </el-form-item>
    </el-form>
  </el-collapse-item>
</template>

<script>
import { urlRE, getURL } from '@/utils/request'

export default {
  data() {
    return {
      methodOptions: ['GET', 'POST', 'PUT', 'DELETE'],
      dataOptions: ['object', 'array', 'string'],
    }
  },
  computed: {
    request() {
      return this.$store.state.curComponent.request
    },
  },
  methods: {
    addArrayData() {
      this.request.data.push('')
    },

    addData() {
      this.request.data.push(['', ''])
    },

    deleteData(index) {
      this.request.data.splice(index, 1)
    },

    onChnage() {
      if (this.request.paramType === 'array') {
        this.request.data = ['']
      } else {
        this.request.data = [['', '']]
      }
    },

    validateURL() {
      const url = this.request.url
      if ((url && /^\d+$/.test(url)) || !urlRE.test(getURL(url))) {
        this.$message.error('请输入正确的 URL')
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.request-container {
  .param-container {
    margin-top: 10px;

    .el-button {
      margin-top: 10px;
    }

    .param-object-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 4px;

      .el-input {
        width: 98px;
      }

      .el-button {
        margin: 0;
        margin-left: 8px;
      }
    }

    .div-delete {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 4px;

      .el-button {
        margin: 0;
        margin-left: 8px;
      }
    }
  }

  .icon-shanchu {
    cursor: pointer;
    margin-left: 10px;
  }
}
</style>
