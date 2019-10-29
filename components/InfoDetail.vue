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
   
  
</div>
</template>
<script>
export default {
    components: {
    },
    props :{
    },
     data(){
        return{
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

    },
 }
</script>
<style scoped>
.v-data-table td{
    height: 30px;
}
</style>
