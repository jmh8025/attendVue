<template>
<div>
 <v-simple-table>
      <tbody>
        <tr v-for="l in Lists" :key="l.name">
          <td>{{ l.key }}</td>
          <td>{{ l.val }}</td>
        </tr>
      </tbody>
  </v-simple-table>
 <div class="text-center">
    <v-btn class="ma-2" tile dark color="indigo" @click="showModal2 = true">
    <v-icon dark>mdi-account-plus</v-icon>사진찍기
  </v-btn>
  <img src="https://attend-smu.mncapro.com/newImage/011700001.jpg" alt="" style="height: 156px; width: 98px;border: 0;">
 </div>
  <div class="text-center">
  <v-btn class="ma-2" tile dark color="indigo" >
    <v-icon dark>mdi-account-plus</v-icon>출석
  </v-btn>
  <v-btn class="ma-2" tile dark color="teal" @click="showList">
    <v-icon dark>mdi-format-list-bulleted</v-icon>리스트 보기
  </v-btn>
  </div>
    <v-row justify="center">
    <v-dialog v-model="showModal2" persistent max-width="290">
      <v-card>
        <v-card-title class="headline">QR검색</v-card-title>
        <v-card-text> 
        <web-cam 
            ref="webcam"
            :device-id="deviceId"
            width="100%"
            @started="onStarted"
            @stopped="onStopped"
            @error="onError"
            @cameras="onCameras"
            @camera-change="onCameraChange"  
        />

            <div class="row">
                    <div class="col-md-12">
                        <select v-model="camera">
                            <option>-- Select Device --</option>
                            <option
                                v-for="device in devices"
                                :key="device.deviceId"
                                :value="device.deviceId"
                            >{{ device.label }}</option>
                        </select> 
                    </div>
                    <div class="col-md-12">
                        <button type="button" class="btn btn-primary" @click="onCapture">Capture Photo</button>
                        <button type="button" class="btn btn-danger" @click="onStop">Stop Camera</button>
                        <button type="button" class="btn btn-success" @click="onStart">Start Camera</button>
                        <button type="button" class="btn btn-success" @click="onCameras">Start onCameras</button>
                        <button type="button" class="btn btn-success" @click="onCameraChange">Start onCameraChange</button>
                    </div>
                </div>
            <div class="col-md-6">
                <h2>Captured Image</h2>
                <figure class="figure">
                    <img :src="img" class="img-responsive" />
                </figure>
            </div>


        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="showModal2 = false">끄기</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
  
</div>
</template>
<script>
import { WebCam } from "vue-web-cam";
export default {
    
    components: {
        WebCam
    },
    props :{
    },
     data(){
        return{
             img: null,
            camera: null,
            deviceId: null,
            devices: [],
            showModal2 : false,
            Lists: [
                {
                    key: '이름',
                    val: '전민호',
                },
                {
                    key: '생년월일',
                    val: '19920630',
                },
                {
                    key: '모집단위',
                    val: '사회심리학과',
                },
                {
                    key: '수험번호',
                    val: '011700001',
                },
                {
                    key: '시험장/(원시험장)	',
                    val: '1 (1)',
                },
            ],
        }
    },
    methods: {
        showList() {
            this.$emit('showStudentList');
        },
        onCapture() {
            this.img = this.$refs.webcam.capture();
        },
        onStarted(stream) {
            console.log("On Started Event", stream);
        },
        onStopped(stream) {
            console.log("On Stopped Event", stream);
        },
        onStop() {
            this.$refs.webcam.stop();
        },
        onStart() {
            this.$refs.webcam.start();
        },
        onError(error) {
            console.log("On Error Event", error);
        },
        onCameras(cameras) {
            this.devices = cameras;
            console.log("On Cameras Event", cameras);
        },
        onCameraChange(deviceId) {
            this.deviceId = deviceId;
            this.camera = deviceId;
            console.log("On Camera Change Event", deviceId);
        }

    },
    mounted() {
    },
     computed: {
        device: function() {
            return this.devices.find(n => n.deviceId === this.deviceId);
        }
    },
    watch: {
        camera: function(id) {
            this.deviceId = id;
        },
        devices: function() {
            // Once we have a list select the first one
            const [first, ...tail] = this.devices;
            if (this.devices.length > 1) {
                this.camera = this.devices[1].deviceId;
                this.deviceId = this.devices[1].deviceId;
            }else if(first){
                this.camera = first.deviceId;
                this.deviceId = first.deviceId;
            }
        }
    },
 }
</script>
<style scoped>
.v-data-table td{
    height: 30px;
}
    #video {
        background-color: #000000;
    }
    #canvas {
        display: none;
    }
    li {
        display: inline;
        padding: 5px;
    }
</style>
