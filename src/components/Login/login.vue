<template>
    <div class="login_container">
        <div class="login_inner_container">
            <div class="login_choices">
                <span class="login" @click="handleFormTypeChange">登录</span>
                <span class="dot">·</span>
                <span class="signIn" @click="handleFormTypeChange">注册</span>
            </div>
            <div class="submit_container">
                <div class="login_submit_container" v-if="currentChoice === '登录'">
                    <input type="text" v-model="loginUsername" placeholder="请输入用户名"  required/>
                    <input type="password" v-model="loginUserPassword" placeholder="请输入密码"  required/>
                </div>
                <div class="signIn_submit_container" v-else>
                    <input type="email" v-model="signInUsername" placeholder="请输入邮箱" required/>
                    <input type="password" v-model="signInUserPassword" placeholder="请输入密码" required/>
                    <input type="password" v-model="confirmPassword" placeholder="请再次确认密码" required/>
                </div>
                <button class="submit_button" @click="handleInfoSubmit">
                    <span class="login_text" v-if="currentChoice === '登录'">这里是诺坎普！请登录</span>
                    <span class="signIn_text" v-else>注册</span>
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: "login",
        data () {
            return {
                currentChoice: '登录',
                loginUsername: '',
                loginUserPassword: '',
                signInUsername: '',
                signInUserPassword: '',
                confirmPassword: ''
            }
        },
        methods: {
            handleFormTypeChange (e) {
                this.currentChoice = e.target.innerText
            },
            handleInfoSubmit () {
                const { currentChoice, loginUsername, loginUserPassword, signInUsername, signInUserPassword, confirmPassword } = this;
                if (currentChoice === '登录') {
                    if (!loginUsername || !loginUserPassword) {
                        alert("用户名或密码不能为空");
                    } else {
                        axios({
                            url: 'http://120.78.172.218:8081',
                            method: 'post',
                            data: {
                                username: loginUsername,
                                userpwd: loginUserPassword
                            }
                        }).then(res => {
                            const { data } = res;
                            alert(data.message);
                        }).catch(err => {
                            console.log(err);
                        })
                    }
                }
            }
        }
    }
</script>

<style scoped lang="scss">
    .login_container{
        height: 100vh;
        position: relative;
        font-size: 100px;
        background: url("../../../public/nuokanpu.jpg") center center no-repeat;
        background-size: cover;
        .login_inner_container{
            padding-top: 32px;
            position: absolute;
            width: 4em;
            height: 5em;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
            box-sizing: border-box;
            border: 1px solid #eeeeee;
            border-radius: 6px;
            box-shadow: 0 0 4px #eeeeee;
            .login_choices{
                font-size: .20em;
                text-align: center;
                span{
                    color: #ffffff;
                    display: inline-block;
                    margin: 0 .12em;
                    line-height: 4;
                    cursor: pointer;
                }
                .dot{
                    display: inline-block;
                    margin: 0 12px;
                    font-size: 20px;
                    font-weight: 900;
                }
            }
            .submit_container{
                div {
                    input {
                        display: block;
                        width: 85%;
                        margin: 36px auto;
                        overflow: hidden;
                        line-height: 2.8;
                        border-radius: 4px;
                        border: 1px solid #cccccc;
                        outline: none;
                        text-indent: .5em;
                    }
                }
                .submit_button{
                    display: block;
                    width: 85%;
                    margin: 18px auto;
                    background-color: rgba(30, 144, 255, .8);
                    border: none;
                    color: #ffffff;
                    line-height: 3;
                    font-size: 16px;
                    border-radius: 4px;
                    cursor: pointer;
                    transition: all .3s ;
                    outline: none;
                    &:hover{
                        box-shadow: 0 0 2px rgba(30, 144, 255, 1);
                    }
                }
            }
        }
    }
</style>