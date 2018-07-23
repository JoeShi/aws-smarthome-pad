<template>
  <el-card :body-style="{ padding: '5px'}" style="margin: 10px; max-width: 400px">
    <img src="../assets/bulb.png" class="image">
    <div style="padding: 14px;">
      <span>确定绑定该设备？</span>
      <div class="bottom clearfix">
        <el-button type="primary" @click.native="bindDevice" :loading="binding">确认绑定</el-button>
      </div>
    </div>
  </el-card>
</template>

<script>
  import { API, Auth } from 'aws-amplify'
  import { Message } from 'element-ui'

  export default {
    name: "device-binding",
    data() {
      return {
        binding: false
      }
    },
    methods: {
      bindDevice: function () {
        const self = this
        self.binding = true
        const thingName = this.$route.params.thingName

        API.post('ThingsCRUD', '/Things', {
          body: {
            thingName: thingName,
            createdOn: new Date(),
            alexaType: 'SmartHome'
          }
        }).then(() => {
          self.binding = false
          this.$message({
            showClose: true,
            message: '绑定成功，如果您使用Alexa,可以说 Alexa, discovery Device..',
            type: 'success'
          });
          console.log('bind successfully')
        }).catch((err) => {
          self.binding = false
          console.error(err)
        })

      }
    }
  }
</script>

<style scoped>
  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }

  .clearfix:after {
    clear: both
  }
</style>
