<template>
<v-container fluid grid-list-md >
    <v-layout row wrap>
        <v-flex sm12 md12 lg6>
            <InfoList />
        </v-flex>
        <v-flex  sm12 md12 lg6 >
            <StudentList />
        </v-flex>
    </v-layout>
</v-container>
</template>

<script>
 import InfoList from '~/components/InfoList';
 import StudentList from '~/components/StudentList';
    export default {
        layout:'user',
        components:{
            InfoList,
            StudentList,
        },
    data(){
        return{
        }
    }
}
</script>

<style  scoped>


</style>