<template>
    <div class="login-component">
        <div class="login-box">
            <div class="login-title"><span class="login-title-L">L</span>ogin</div>
            <div>
                <div class="login-input-botton">
                    <v-text-field v-model="json.username" label="Id" placeholder="Placeholder" dense outlined></v-text-field>
                    <v-text-field v-model="json.password" type="password" label="Password" placeholder="Placeholder" dense outlined></v-text-field>
                </div>
                <div><v-btn @click="login" color="#81C784" elevation="2" class="login-button">로그인</v-btn></div>
            </div>
        </div>
    </div>
</template>
<script>
// import { loginUser } from '@/api/core/index';

export default {
    data() {
        return {
            json: {
                username: '',
                password: '',
            },
        };
    },
    components: {
        // Main
    },
    // mounted() {
    //     if (sessionStorage.getItem('isLogin') == 'true') {
    //         this.$router.push('/');
    //     }
    // },
    methods: {
        login() {
            const userinfo = {
                username: this.json.username,
                password: this.json.password,
            };
            if (this.json.username == '') {
                alert('아이디를 입력해주세요.');
                return;
            } 
            
            console.log(userinfo);
            this.$http
                .post('https://localhost:8086/login', userinfo, {
                    withCredentials: true,
                })
                .then((res) => {
                    // this.test = response.data;
                    console.log(res);
                    // state에 회원 정보 담기
                    this.$store.commit('userStore/userInfo', userinfo);
                    this.$http
                        .get('/api/user', {
                            withCredentials: true,
                        })
                        .then((res) => {
                            // state에 저장
                            const userData = {
                                caresitterId: res.data.body.careSitterId,
                                storeId: res.data.body.storeId,
                            };
                            console.log(userData);
                            this.$store.commit('userStore/userData', userData);
                            // console.log(this.$store.state.userStore.name);
                            location.href = '/';
                        })
                        .catch((err) => {
                            console.log(err);
                            console.log(this.json);
                        });
                })
                .catch((err) => {
                    console.log(err);
                    console.log(this.json);
                });
        },
    },
};
</script>

<style scoped lang="scss">
.main {
    min-height: 100vh;
}
.login-component {
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%); // x축 y축
    width: 300px;
    height: 500px;
    background: white;
    box-shadow: 5px 5px 5px 5px #c4c4c4;
    border-radius: 11px;
}
.login-box {
    padding: 15% 8%;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    align-items: center;
    height: 100%;
}
.login-title {
    font-family: jost;
    font-size: 30px;
    color: #81C784;
}
.login-title-L {
    font-family: jost;
    font-size: 40px;
    color: #81C784;
}
.login-input-button {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.login-button {
    margin-top: 10%;
    width: 100%;
}
.idpwfind{
    position: relative;
    left: 110px;
    top: 10px;
}
</style>
