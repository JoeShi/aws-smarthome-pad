/*
 * Copyright 2017-2017 Amazon.com, Inc. or its affiliates. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License"). You may not use this file except in compliance with
 * the License. A copy of the License is located at
 *
 *     http://aws.amazon.com/apache2.0/
 *
 * or in the "license" file accompanying this file. This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
 * CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions
 * and limitations under the License.
 */

<template>
  <div>
    <el-row>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_light_on.png" class="image">
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 12px">
              <div>
                <span>客厅灯</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_light_on.png" class="image">
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 12px">
              <div>
                <span>卧室灯</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_air_purifier.png" class="image">
              <div class="label">卧室</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">86</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_flower.png" class="image">
              <div class="label">百合</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">123</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_air_conditioner.png" class="image">
              <div class="label">卧室</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">27</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card :body-style="{ padding: '16px'}" class="card">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_iRobot.png" class="image">
              <div class="label">iRobot</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 20px">
              <div>
                <span style="font-size: 1em">打扫中</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
  .label {
    color: gray;
  }
  .card {
    margin: 15px;
  }
  .image {
    display: inline;
    width: 64px;
    height: 64px;
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

<script>
import { AmplifyTheme } from '../amplify'

export default {
  name: 'Home',
  data () {
    return {
      theme: AmplifyTheme,
      things: [
        {
          type: 'light',
          status: 'on',
          location: '客厅',
          thingName: '1'
        },
        {
          type: 'light',
          status: 'off',
          location: '卧室',
          thingName: '2'
        },
        {
          type: 'airPurifier',
          status: 'on',
          location: '卧室',
          thingName: '3'
        },
        {
          type: 'moisture',
          status: 'on',
          location: '阳台',
          name: '百合',
          thingName: '4'
        },
        {
          type: 'airConditioner',
          status: 'on',
          location: '卧室',
          thingName: '5'
        },
        {
          type: 'iRobot',
          status: 'on',
          location: '卧室',
          thingName: '6'
        }
      ]
    }
  }
}
</script>
