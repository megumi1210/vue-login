<template>
    <div class="container">

        <div class="header">
            <div class="nav">

                <div class="logo"></div>

                <div class="right">
                    <span><b>申请使用</b></span>
                    <span><b>官网</b></span>
                    <span><b>周边</b></span>
                    <span><b>帮助</b></span>
                    <span><b>公众号</b></span>
                </div>
            </div>
        </div>

        <div class="main">
            <div class="content">
                <div class="main-top">
                    <div class="banner">
                        <img style="width: 560px; margin:0 ;padding: 0"
                             src=" https://schoolpal.oss-cn-hangzhou.aliyuncs.com/erpbanner/erplogin0827.jpg" alt=""/>
                    </div>

                    <div class="login-form">

                        <div style="display: flex; justify-content: space-between;margin-top: 60px; height:50px">

                            <div style="display: flex; align-items: center ; flex-direction: column;">
                                <span  :class="phoneActive?'msg_title active':'msg_title notActive'"  @click="changeForm('PhoneLogin')">手机号码登录</span>
                                <div  class="sub_form_title" v-show="phoneActive"></div>
                            </div>

                            <div style="display: flex; align-items: center ; flex-direction: column;">
                                <span :class="phoneActive?'msg_title notActive':'msg_title active'" @click="changeForm('UserLogin')">账号登录</span>
                                <div class="sub_form_title" v-show="!phoneActive"></div>
                            </div>
                        </div>

                        <div class="form" v-if="phoneActive" style="margin-bottom: 60px" >
                            <div class="form-group" >
                                <input  v-model="phoneNum" :class="phoneNumMsgShow?'errorInput':phoneNumNormal?'normalInput':'activeInput'" type="text"
                                        placeholder="请输入手机号码" v-on:keyup="phoneNumCheck()"  v-on:focus="phoneNumActive">
                                <span  v-show="phoneNumMsgShow"  class="errorMsg">{{phoneNumMsg}}</span>
                            </div>

                            <div class="form-group" style="margin-top: 30px">
                                <input v-model="phonePass" type="password" :class="phonePassMsgShow?'errorInput':phonePassNormal?'normalInput':'activeInput'" placeholder="请输入密码"  v-on:keyup="phonePassCheck()"  v-on:focus="phonePassActive()">
                                <span  v-show="phonePassMsgShow" class="errorMsg">{{phonePassMsg}}</span>
                            </div>
                        </div>


                        <div class="form" v-if="!phoneActive">

                            <div class="form-group">
                                <input  v-model="institution" :class="institutionMsgShow?'errorInput':institutionNormal?'normalInput':'activeInput'" type="text" placeholder="请输入机构后缀"  v-on:keyup="institutionCheck()"  v-on:focus="institutionActive()">
                                <span  v-show="institutionMsgShow" class="errorMsg">{{institutionMsg}}</span>
                            </div>


                            <div class="form-group">
                                <input  v-model="username" type="text"  :class="usernameMsgShow?'errorInput':usernameNormal?'normalInput':'activeInput'" placeholder="请输入登录名" v-on:keyup="usernameCheck()"  v-on:focus="usernameActive()">
                                <span  v-show="usernameMsgShow" class="errorMsg">{{usernameMsg}}</span>
                            </div>

                            <div class="form-group">
                                <input v-model="userPass" type="password" :class="userPassMsgShow?'errorInput':userPassNormal?'normalInput':'activeInput'" placeholder="请输入密码"  v-on:keyup="userPassCheck()"  v-on:focus="userPassActive()">
                                <span  v-show="userPassMsgShow" class="errorMsg">{{userPassMsg}}</span>
                            </div>
                        </div>



                        <button class="btn" :class="phoneActive?phoneFormValid?'btnEnabled':'btnDisabled':userFormValid?'btnEnabled':'btnDisabled'"  :disabled="phoneActive?phoneFormValid:userFormValid"  @click="doLogin()">登录</button>
                    </div>
                </div>

                <div class="main-footer">
                    <div class="left-item">
                        <span><b>相关产品</b></span>
                        <div style="margin-top: 5px">
                            <div class="item">
                                <div>
                                    <img src="https://prox.schoolpal.cn/common/images/icon-scp.png" alt=""/>
                                </div>
                                <div class="tip">
                                    <span class="title"><b>校宝收银宝</b></span>
                                    <span class="sub_title">学校收费标配</span>
                                </div>
                            </div>

                            <div class="item">
                                <div>
                                    <img src="https://prox.schoolpal.cn/common/images/icon-zhaoshengbao.png" alt=""/>
                                </div>
                                <div class="tip">
                                    <span class="title"><b>校宝招生宝</b></span>
                                    <span class="sub_title">一站招生服务</span>
                                </div>
                            </div>

                            <div class="item">
                                <div>
                                    <img src="https://prox.schoolpal.cn/common/images/icon-anxinbao.png" alt=""/>
                                </div>
                                <div class="tip">
                                    <span class="title"><b>校宝安心宝</b></span>
                                    <span class="sub_title">教育保险精选</span>
                                </div>
                            </div>

                        </div>
                    </div>

                    <div class="right-item">
                        <div>
                            <span><b>咨询热线</b></span>
                        </div>

                        <div style="margin-right: 10px; margin-bottom: 20px">
                            <span style="font-size: 28px"><b>400-6999-707</b></span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>


    export default {
        name: "Login",
        data() {
            return {
                phoneNum:'',
                phonePass:'',
                institution:'',
                username:'',
                userPass:'',
                currentForm: 'PhoneLogin',
                phoneActive: true,
                phoneNumMsg:'',
                phoneNumMsgShow:false,
                phonePassMsg:'',
                phonePassMsgShow:false,
                institutionMsg:'',
                institutionMsgShow:false,
                usernameMsg:'',
                usernameMsgShow:false,
                userPassMsg:'',
                userPassMsgShow:false,
                phoneNumNormal:true,
                phonePassNormal:true,
                institutionNormal:true,
                usernameNormal:true,
                userPassNormal:true,
                phoneFormValid:false,
                userFormValid:false

            }
        },
        methods: {
            changeForm(formName) {
                this.currentForm = formName;
                this.phoneActive = !this.phoneActive
            },
            phoneNumCheck(){
                 let valid = true;
                if(this.phoneNum.length===0){
                    this.phoneNumMsgShow =true;
                    this.phoneNumMsg='请输入手机号';
                    valid=false;
                    this.phoneFormValid=false
                }

                if(this.phoneNum.length !== 11 && valid){
                    this.phoneNumMsgShow =true;
                    this.phoneNumMsg='请输入正确的手机号';
                    this.phoneFormValid=false;
                }

               if(this.phoneNum.length === 11){
                   this.phoneNumMsgShow =false;
                  this.phoneFormCheck()
               }
                this.phoneNumNormal =true

            },
            phoneNumActive(){
                this.phoneNumNormal=false
            },
            phonePassCheck(){
                if(this.phonePass === ''){
                    this.phonePassMsgShow=true;
                    this.phonePassMsg='请输入密码';
                    this.phoneFormValid =false
                }
                if(this.phonePass.length !== 0){
                    this.phonePassMsgShow =false;
                     this.phoneFormCheck()
                }
                this.phonePassNormal =true
            },
            phonePassActive(){
                this.phonePassNormal=false
            },
            institutionCheck(){
                if(this.institution === ''){
                    this.institutionMsgShow =true;
                    this.institutionMsg='请输入机构名';
                    this.userFormValid =false
                }

                if(this.institution.length !== 0){
                    this.institutionMsgShow =false;
                    this.userFormCheck()
                }
                this.institutionNormal =true
            },
            institutionActive(){
                this.institutionNormal=false
            },
            usernameCheck(){
                if(this.username === ''){
                    this.usernameMsgShow =true;
                    this.usernameMsg='请输入用户名';
                    this.userFormValid =false;
                }

                if(this.username.length !== 0){
                    this.usernameMsgShow =false;
                    this.userFormCheck()
                }
                this.usernameNormal =true
            },
            usernameActive(){
                this.usernameNormal=false
            },
            userPassCheck(){
                if(this.userPass === ''){
                    this.userPassMsgShow=true;
                    this.userPassMsg='请输入密码';
                    this.userFormValid =false;
                }
                if(this.userPass.length !== 0){
                    this.userPassMsgShow =false;
                    this.userFormCheck()
                }
                this.userPassNormal =true
            },
            userPassActive(){
                this.userPassNormal=false
            },
            doLogin(){
                let valid = true;
                if(this.phoneActive){//通过手机号登陆


                     if(this.phoneNum === ''){
                         this.phoneNumMsgShow =true;
                         this.phoneNumMsg='请输入手机号';
                         valid=false
                     }

                    if(this.phoneNum.length !== 11 && valid){
                        this.phoneNumMsgShow =true;
                        this.phoneNumMsg='请输入正确的手机号';
                        valid=false
                    }

                    if(this.phonePass === ''){
                        this.phonePassMsgShow=true;
                        this.phonePassMsg='请输入密码';
                        valid=false
                    }

                    if(valid){
                        console.log(this.phoneNum +"---" +this.phonePass)
                    }

                }else {//机构登陆
                    if(this.institution === ''){
                        this.institutionMsgShow =true;
                        this.institutionMsg='请输入机构名';
                        valid=false
                    }

                    if(this.username === ''){
                        this.usernameMsgShow =true;
                        this.usernameMsg='请输入用户名';
                        valid=false
                    }

                    if(this.userPass === ''){
                        this.userPassMsgShow=true;
                        this.userPassMsg='请输入密码';
                        valid=false
                    }
                }
            },
            phoneFormCheck(){
                if(this.phoneNum.length===11 && this.phonePass!==''){
                    this.phoneFormValid=true
                }
            },
            userFormCheck(){
                if(this.institution !=='' && this.username !=='' && this.userPass!==''){
                    this.userFormValid=true
                }
            }
        }
    }


</script>

<style>



    .normalInput{
        width: 340px;
        height: 24px;
        font-size: 14px;
        border-style: none;
        outline: none;
        margin-left: 32px;
        border-bottom: 1px solid grey;
        margin-bottom: 5px;
    }

    .activeInput{
        width: 340px;
        height: 24px;
        font-size: 14px;
        border-style: none;
        outline: none;
        margin-left: 32px;
        margin-bottom: 5px;
        border-bottom: 2px solid #007AFF;
    }

    .errorInput{
        width: 340px;
        height: 24px;
        font-size: 14px;
        border-style: none;
        outline: none;
        margin-left: 32px;
        margin-bottom: 5px;
        border-bottom: 2px solid #ff3366;
    }



    .container {
        width: 100%;
        height: 100%;
        padding: 0;
        border: 0;
        margin: 0;
    }

    .header {
        width: 100%;
        display: flex;
        justify-content: center;
        padding: 0;
        background-color: #fff;

    }

    .logo {
        height: 60px;
        padding-top: 0;
        width: 200px;
        background-image: url("https://cdn.schoolpal.cn/schoolpal/resource/ci/SchoolPal-NETCore-PC/130/common/images/icon-loginlogo-new.jpg?version=20201022223932");
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
    }

    .nav {
        display: flex;
        justify-content: space-between;
        width: 1000px;
    }



    .right {
        margin-top: 12px;
    }

    .nav span {
        width: 80px;
        font-size: 16px;
        height: 60px;
        padding-bottom: 12px;
        margin-right: 10px;

    }

    .nav span:hover {
        color: #007AFF;
        border-bottom: 2px solid #007AFF;
        border-bottom-width: 4px;
    }

    .nav {
        display: flex;
    }


    .main {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        text-align: center;
    }

    .content {
        width: 1000px;
    }

    .banner img {
        width: 560px;
        border-bottom-left-radius: 8px;
        border-top-left-radius: 8px;
    }


    .main-top {
        display: inline-flex;
        border-radius: 8px;
    }

    .login-form {
        width: 440px;
        background-color: white;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }

    .main-footer {
        width: 100%;
        display: flex;
        justify-content: space-between;
        text-align: justify;
        margin-top: 10px;
    }

    .item {
        display: inline-flex;
        background-color: #F5CBCF;
        margin-top: 5px;
        width: 210px;
        height: 60px;
        margin-right: 10px;
        border-radius: 8px;

    }

    .item img {
        height: 60px;
    }

    .item:hover {
        background-color: #eaedf2;
        margin-top: 2px;
    }

    .tip {
        display: flex;
        flex-direction: column;
    }

    .title {
        font-size: 16px;
    }

    .sub_title {
        font-size: 13px;
    }

    .btnEnabled {
        width: 320px;
        height: 54px;
        font-size: 16px;
        background-color: #007AFF;
        border-style: none;
        outline: none;
        color: #fff;
        border-radius: 30px;
        margin-bottom: 30px;

    }

     .btnDisabled {
         width: 320px;
         height: 54px;
         font-size: 16px;
         background-color: #cccccc;
         border-style: none;
         outline: none;
         color: #fff;
         border-radius: 30px;
         margin-bottom: 30px;

     }

    .login-form .btnEnabled:hover {
        background-color: #006EE7;
        cursor: pointer;

    }


    .sub_form_title {
        background-color: #007AFF;
        width: 32px;
        height: 5px;
        border-radius: 4px;
        margin-top: 10px;
    }


    .right-item {
        display: flex;
        flex-direction: column;
        justify-content: space-between;

    }


    .errorMsg {
        color: #ff3366;
        font-size: 12px;
        text-align: right;
        line-height: 12px;

    }

    .active {
        font-size: 18px;
        width: 150px;
        opacity: 100%;
    }

    .notActive {
        font-size: 18px;
        width: 150px;
        opacity: 50%;
    }

    .msg_title:hover{
        cursor: pointer;
    }






    .form{
        display: flex;
        flex-direction: column;
    }


    .form-group {
        display: flex;
        flex-direction: column;
        margin-bottom: 30px;
        height: 50px;
    }



</style>