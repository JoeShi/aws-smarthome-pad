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
    <el-row v-for="row in Math.ceil(things.length/4)" :key="row">
      <el-col :span="6" v-for="index in 4" :key="index" v-if="index - 1 + (row -1) * 4 < things.length">
        <!--{{ index - 1 + (row -1) * 4 }}-->
        <!-- light -->
        <el-card :body-style="{ padding: '16px'}" class="card" v-if="things[index - 1 + (row -1) * 4].type === 'light'"
                  @click.native="togglePower(index - 1 + (row -1) * 4)">
          <el-row>
            <el-col :span="12">
              <img v-if="things[index - 1 + (row -1) * 4].status === 'on'" src="../assets/icon_light_on.png" class="image">
              <img v-else src="../assets/icon_light_off.png" class="image">
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 12px">
              <div>
                <span>{{ things[index - 1 + (row -1) * 4].location }}</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
        <!-- air purifier -->
        <el-card :body-style="{ padding: '16px'}" class="card" v-if="things[index - 1 + (row -1) * 4].type === 'airPurifier'">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_air_purifier.png" class="image">
              <div class="label">{{ things[index - 1 + (row -1) * 4].location }}</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">86</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
        <!-- moisture -->
        <el-card :body-style="{ padding: '16px'}" class="card" v-if="things[index - 1 + (row -1) * 4].type === 'moisture'">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_flower.png" class="image">
              <div class="label">{{ things[index -1 + (row-1) * 4].name }}</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">{{ things[index -1 + (row-1) * 4].state.reported.value}}</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
        <!-- air conditioner -->
        <el-card :body-style="{ padding: '16px'}" class="card" v-if="things[index - 1 + (row -1) * 4].type === 'airConditioner'"
                  @click.native="goTo(index - 1 + (row -1) * 4)">
          <el-row>
            <el-col :span="12">
              <img src="../assets/icon_air_conditioner.png" class="image">
              <div class="label">{{ things[index - 1 + (row -1) * 4].location }}</div>
            </el-col>
            <el-col :span="12" style="padding: 12px; margin-top: 10px">
              <div>
                <span style="font-size: 2.5em">27</span>
              </div>
            </el-col>
          </el-row>
        </el-card>
        <!-- iRobot -->
        <el-card :body-style="{ padding: '16px'}" class="card" v-if="things[index - 1 + (row -1) * 4].type === 'iRobot'">
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
import Amplify, { PubSub } from 'aws-amplify'
import { AWSIoTProvider } from 'aws-amplify/lib/PubSub/Providers'

export default {
  name: 'Home',
  data () {
    return {
      theme: AmplifyTheme,
      things: [
        {
          type: 'light',
          location: '卧室',
          thingName: 'home-1-lamp',
          status: 'off'
        },
        {
          type: 'light',
          location: '客厅',
          thingName: 'bulb-s00000002',
          status: 'off'
        },
        {
          type: 'airPurifier',
          location: '卧室',
          thingName: 'home-1-airPurifier',
          state: {
            reported: {
              status: 'off',
              value: 0
            }
          }
        },
        {
          type: 'moisture',
          location: '阳台',
          name: '百合',
          thingName: 'home-1-moisture',
          state: {
            reported: {
              value: 0
            }
          }
        },
        {
          type: 'airConditioner',
          status: 'on',
          location: '卧室',
          thingName: 'home-1-airConditioner',
          state: {
            reported: {
              value: 0,
              status: 'off'
            }
          }
        },
        {
          type: 'iRobot',
          status: 'on',
          location: '卧室',
          thingName: '6'
        }
      ]
    }
  },
  created() {
    console.log('created....')
    Amplify.addPluggable(new AWSIoTProvider({
      aws_pubsub_region: 'us-west-2',
      aws_pubsub_endpoint: 'wss://abty4kifln98q.iot.us-west-2.amazonaws.com/mqtt'
    }))
    const self = this

    self.things.forEach(thing => {
      switch (thing.type) {
        case 'light':
          // subscribe to shadow reported
          PubSub.subscribe(
            [
              `$aws/things/${thing.thingName}/shadow/update/accepted`,
              `$aws/things/${thing.thingName}/shadow/get/accepted`
            ], {}).subscribe({
            next: data => {
              const state = data.value.state
              if (state.reported && state.reported.status) {
                thing.status = state.reported.status // update the status
              }
            },
            error: error => {
              console.error(error)
            },
            close: () => console.log('Done')
          })
          // get the shadow status
          PubSub.publish(`$aws/things/${thing.thingName}/shadow/get`, {}, null)
          break
        case 'airPurifier':
          PubSub.subscribe(
            [
              `$aws/things/${thing.thingName}/shadow/update/accepted`,
              `$aws/things/${thing.thingName}/shadow/get/accepted`
            ], {}).subscribe({
            next:  data => {
              const state = data.value.state
              if (state.reported) {
                if (state.reported.status) {
                  thing.state.reported.status = state.reported.status
                }
                if (state.reported.value) {
                  thing.state.reported.value = state.reported.value
                }
                // console.log(thing.state.reported)
              }
            },
            error: error => {
              console.error(error)
            },
            close: () => console.log('Done')
          })
          // get the shadow status
          PubSub.publish(`$aws/things/${thing.thingName}/shadow/get`, {}, null)
          break
        case 'moisture':
          PubSub.subscribe(
            [
              `$aws/things/${thing.thingName}/shadow/update/accepted`,
              `$aws/things/${thing.thingName}/shadow/get/accepted`
            ], {}).subscribe({
            next:  data => {
              const state = data.value.state
              if (state.reported) {
                thing.state = state
              }
            },
            error: error => {
              console.error(error)
            },
            close: () => console.log('Done')
          })
          // get the shadow status
          PubSub.publish(`$aws/things/${thing.thingName}/shadow/get`, {}, null)
          break
        case 'airConditioner':
          break
        case 'iRobot':
          break
        default:
          console.info('unknown device')
      }
    })

    // PubSub.subscribe('myTopic').subscribe({
    //   next: data => console.log('Message received', data),
    //   error: error => console.error(error),
    //   close: () => console.log('Done'),
    // })
  },
  methods: {
    togglePower(index) {
      console.log('toggle power')
      const self = this
      const thing = self.things[index]
      const message = {
        state: {
          desired: {
            status: 'on'
          }
        }
      }
      if (thing.status === 'on') {
        message.state.desired.status = 'off'
      }

      PubSub.publish(`$aws/things/${thing.thingName}/shadow/update`, message, null)
    },
    goTo(index) {
      const self = this
      const thing = self.things[index]
      if (thing.type === 'airConditioner') {
        self.$router.push({ path: `/airConditioners/${thing.thingName}`})
      }
    }
  }
}
</script>
