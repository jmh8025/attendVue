<template>
    <v-container class="fill-height" fluid>
            <v-row align="center" justify="center">
            <v-col cols="12" sm="8" md="4" >
                
                <v-card class="elevation-12">
                    <v-form ref="form" v-model="valid" @submit.prevent="onSubmitForm">
                        <v-toolbar flat>
                            <v-toolbar-title><v-img src='/img/logo.png'></v-img></v-toolbar-title>
                            <v-spacer></v-spacer>
                        </v-toolbar>
                        <v-card-text>
                            <v-select
                                :items="period"
                                :rules="periodRules"
                                label="교시선택"
                                outlined
                            />
                            <v-text-field
                                v-model="id"
                                :rules="idRules"
                                label="아이디"
                                prepend-icon="mdi-account"
                                type="text"
                                required
                            />
                            <v-text-field
                                v-model="password"
                                :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                                :rules="passwordRules"
                                :type="showPassword ? 'text' : 'password'"
                                label="비밀번호"
                                class="input-group--focused"
                                prepend-icon="mdi-lock-question"
                                @click:append="showPassword = !showPassword"
                                style="ime-mode:disabled"
                                required
                            />
                        </v-card-text>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <div class="my-2">
      
                            <v-btn 
                                depressed 
                                large 
                                :disabled="!valid"
                                color="primary"
                                rounded 
                                type="submit" 
                                
                            >로그인</v-btn>
                            </div>
                            <v-spacer></v-spacer>
                        </v-card-actions>
                    </v-form>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
     data(){
        return{
            period : ['1교시','2교시'],
            showPassword : false,
            valid: false,
            periodRules :[
                v => !!v || '교시선택은 필수입니다.',
            ],
            id: '',
            idRules: [
                v => !!v || '아이디는 필수입니다.',
                v => v.length <= 10 || '아이디는 10자리 이하입니다.',
            ],
            password: '',
            passwordRules: [
                v => !!v || '비밀번호는 필수입니다.',
                v => v.length >= 8 || '비밀번호는 8자리 이상입니다.',
                v => /[~!@\#$%<>^&*]/.test(v) || '비밀번호에 [~!@\#$%<>^&*]가 포함되어야합니다.',
                v => /[a-zA-Z]/.test(v) || '비밀번호에 영문자가 포함되어야합니다.',
                v => /[0-9]/.test(v) || '비밀번호에 숫자가 포함되어야합니다.',
            ],
        }
    },
    methods: {
        onSubmitForm(){
            console.log(this.$refs.form)
            if(this.$refs.form.validate()){
                 this.$router.push({
                         path : '/attendList',
                });
                // this.$store.dispatch('users/signUp', {
                //     nickname : this.nickname,
                //     email : this.email,
                // })
                // .then(() => {
                //     this.$router.push({
                //         path : '/',
                //     });
                // })
                // .catch(()=>{
                //     alert('회원가입실패')
                // })
            }else{
                alert("입력값을 확인하세요.");
            }
        }
    },
 }
</script>
<style scoped>
</style>
