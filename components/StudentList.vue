<template>
<v-card >
   
    <v-app-bar 
        :fixed="appBarFixed"
        hide-on-scroll
        scroll-threshold="100"
        v-scroll="onScroll"
        
    >
        <v-toolbar-title>
            <v-btn color="primary" @click="showModal = true">
                <v-icon>mdi-qrcode-scan</v-icon>
                <div>QR검색</div>
            </v-btn>
        </v-toolbar-title>
        <v-spacer></v-spacer>
        <v-text-field 
            v-model="search"
            append-icon="mdi-account-search"
            label="이름 및 수험번호 입력"
            single-line
            hide-details
            v-on:input="searchTyping"
        ></v-text-field>
    </v-app-bar>
    
    <template  v-if="detailInfo">
    <v-data-table 
        v-if="detailInfo"
        :mobile-breakpoint='NaN'
        :headers="headers"
        :items="Lists"
        :search="search"
        open-on-click
        :no-results-text="noResult"
        hide-default-footer
        disable-sort
        disable-pagination
    >
     <template v-slot:item="props">
         <tr class="text-center" @click="selectDetail(props.item)">
          <td >{{ props.item.no }}</td>
          <td >{{ props.item.name }}</td>
          <td >{{ props.item.birth }}</td>
          <td >{{ props.item.suhumNo }}</td>
          <td >{{ props.item.unit }}</td>
        </tr>
     </template>
    </v-data-table>
    </template>
    <template  v-else>
        <InfoDetail :detailInfo="detailInfo" @showStudentList="showStudentList" />
    </template>

    <div class="text-center">
        <v-snackbar
        color="primary"
        v-model="snackbar"
        :timeout="timeout"
        >
        {{ text }}
        </v-snackbar>
    </div>


    <v-row justify="center">
    <v-dialog v-model="showModal" persistent max-width="290">
      <v-card>
        <v-card-title class="headline">QR검색</v-card-title>
        <v-card-text> <qrcode-stream @decode="onDecode"></qrcode-stream></v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="showModal = false">끄기</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>

</v-card>
</template>


<script>
import InfoDetail from '~/components/InfoDetail';     
import { QrcodeStream, QrcodeDropZone, QrcodeCapture } from 'vue-qrcode-reader'

const MyComponent = {
  components: {
    
  },
};
export default {
    components:{
        InfoDetail,
        QrcodeStream,
        QrcodeDropZone,
        QrcodeCapture
    },
    data(){
        return{
            snackbar: false,
            text: '타 고사장 학생입니다.',
            timeout: 1500,
            showModal: false,
            hideOnScroll : false,
            appBarFixed : false,
            loadingFlag : true,
            detailInfo : true,
            noResult:"이름 및 수험번호를 확인하세요.",
            search: '',
            headers: [
                {
                    text: 'No',
                    align: 'center',
                    sortable: false,
                    value: 'no',
                },
                { text: '이름', value: 'name',align: 'center', },
                { text: '생년월일', value: 'birth',align: 'center', },
                { text: '수험번호', value: 'suhumNo',align: 'center', },
                { text: '모집단위', value: 'unit',align: 'center', },
            ],
            Lists: [
                {
                    no: '1',
                    name: '남상범',
                    birth: '1992-06-30',
                    suhumNo: '920630',
                    unit: '엠엔씨부',
                },
                {
                    no: '2',
                    name: '전민호',
                    birth: '1992-06-30',
                    suhumNo: '2222',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '3',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '3333',
                    unit: '엠엔씨부',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                },{
                    no: '99',
                    name: '진창량',
                    birth: '1992-06-30',
                    suhumNo: '9999',
                    unit: '엠엔씨부이',
                }
                
            ],
        }
    },
    methods: {
        selectDetail(){
            this.detailInfo = false;
            this.snackbar = true;
            this.appBarFixed = false;
        },
        searchTyping : function(e){
            if(this.search != ''){
                this.detailInfo = true;
            }
        },
        showStudentList() {
           this.detailInfo = true;
           this.search = '';
          
        },
        onScroll(e){
            if(window.scrollY >= 300){
                this.appBarFixed = true;
            }else{
                this.appBarFixed = false;
            }
        },
        onDecode (decodedString) {
            // alert(decodedString)
            this.search = decodedString;
            showModal = false;
        }
    },
    fetch(){
    },
}
</script>
<style>
.v-data-table td{
    padding : 0 8px;
}
.v-data-table td{
    height: 30px;
}
</style>
