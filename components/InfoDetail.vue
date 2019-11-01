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


             <web-cam />




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
            video: {},
            canvas: {},
            captures: [],
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
        capture() {
            this.canvas = this.$refs.canvas;
            var context = this.canvas.getContext("2d").drawImage(this.video, 0, 0, 640, 480);
            this.captures.push(canvas.toDataURL("image/png"));
        }

    },
    mounted() {
        this.video = this.$refs.video;
        if(navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
            navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
                this.srcObject = stream; 
                this.video.play();
            });
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
