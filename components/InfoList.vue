<template>
  <v-card >
 <v-simple-table>
    <template v-slot:default>
      <tbody>
        <tr v-for="l in Lists" :key="l.name">
          <td>{{ l.key }}</td>
          <td>{{ l.val }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  </v-card>
</template>
<script>
export default {
    components: {
    },
     data(){
        return{
            Lists: [
                {
                    key: '교시',
                    val: '159',
                },
                {
                    key: '시험장',
                    val: '1',
                },
                {
                    key: '감독관',
                    val: '프라임관 눈꽃광장',
                },
                {
                    key: '출석 / 정원',
                    val: '239명  /  220명',
                },
            ],
        }
    },
    methods: {
    },
 }
</script>
<style scoped>
</style>
