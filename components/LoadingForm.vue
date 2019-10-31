<template>
    <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
        <v-col cols="12" sm="12" md="4" >
            
            <div style="text-align: center;">    
                <transition 
                    name="fade" 
                    v-on:after-enter="afterLogo"
                > 
                    <img ref="logo" v-show="logoShow" width="50%" src='~assets/img/big_logo.png' />
                </transition> 
            </div>
            <div style="text-align: center;" v-show="loadingShow">
                <img  width="10%"  src='~assets/img/loading.gif' />
            </div>

            <transition 
                name="fade-login" 
                v-on:after-leave="afterLoginForm"
            >
            <v-card class="elevation-12" v-show="loginFormShow">
                <v-form ref="form" v-model="valid" @submit.prevent="onSubmitForm">
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
            </transition>
        </v-col>
    </v-row>
    </v-container>
</template>
<script>

export default {
     data(){
        return{
            logoShow : false,
            loadingShow : false,
            loginFormShow : false,
            flag : false,
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
            if(this.$refs.form.validate()){
                this.loginFormShow=false;
            }else{
                alert("입력값을 확인하세요.");
            }
        },
        afterLogo(el,done){
             setTimeout(()=>{
                el.style.transform = `translateY(-167px)`;
                el.style.transition = `all 1s ease`;
                this.afterLogo2(el,done);
                // done();
             }, 2500);
        },
        afterLogo2(el,done){
            setTimeout(()=>{
                el.style.transform = `translateY(0px)`;
                el.style.transition = `all 0s`;
                this.loginFormShow=true;
                done();
            },1500);
        },
        fadeLogo(){
            this.logoShow=true;
        },
        afterLoginForm(){
            
            this.$refs.logo.style.transform = `translateY(-167px)`;
            setTimeout(()=>{
                this.$refs.logo.style.transform = `translateY(0px)`;
                this.$refs.logo.style.transition = `all 1s ease`;
                this.goList();
            },300);
            setTimeout(()=>{
                this.$router.push({
                    path : '/attendList',
                });
            },4000);
        }
    },
    mounted() { 
        setTimeout(this.fadeLogo, 500)
    },
    created: function() {
         this.$nextTick(function() {
              
        });
    },
 }
</script>
<style>
.fade { 
    transition: all 1s;
} 
.fade-enter-active { 
    transition: all 1s ease; 
} 
.fade-leave-active { 
    transition: all 1s cubic-bezier(1, 0.5, 0.8, 1); 
} 
.fade-enter, 
.fade-leave-active { 
    opacity: 0;  
}


.fade-login { 
    transition: all 1s;
} 
.fade-login-enter-active { 
    transition: all 1s ease; 
} 
.fade-login-leave-active { 
    transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1); 
} 
.fade-login-enter,
.fade-login-leave-active { 
    opacity: 0; 
}

</style>
