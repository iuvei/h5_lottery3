<template>
    <div id="pa_con" class="so-con warp">
        <header id="pa_head" class="new_header">
            <div class="left">
                <a href="javascript:;" onclick="history.go(-1)" >
                    <span class="icon icon_back"></span>
                </a>
            </div>
            <h2 class="center title_name">帐户管理</h2>
            <div class="right"></div>
        </header>
        <div class="pa_content">
            <div class="info_area">
                <div class="info_top">
                    <div class="account">
                        <!--<a href="info_data.html">-->
                            <!-- <h2 class="ui header center aligned">
                                <div class="portrait">
                                    <div class="portrait_outline"></div>
                                    <div class="user_portrait"></div>
                                </div>
                            </h2> -->
                            <div class="user_name">
                                <span class="icon icon_user"></span>
                                <strong>{{loginName}}</strong>
                                <div class="purse">
                                    <span class="icon icon_money"></span>
                                    <div class="so-in-top-sum">{{memberbalance}}

                                    </div>
                                </div>
                            </div>
                        <!--</a>-->
                    </div>
                </div>
                <div class="info_mid">
                    <div>
                        <div class="lgps filter_1">
                            <a class="new_btn"><span class="midunm">修改登录密码</span></a>
                        </div>
                        <div class="pps filter_2">
                            <a class="new_btn"><span class="midunm">修改取款密码</span></a>
                        </div>
                    </div>
                </div>
                <div class="page_box">
                    <div class="new_panel info_account">
                        <div class="new_panel_top">帐号安全</div>
                        <div class="new_panel_center print_data">
                            <table>
                                <thead>
                                <tr>
                                    <th class="bank_card_num">
                                        <li>银行卡号</li>
                                    </th>
                                    <td>
                                        {{bankName}}<br/>
                                        {{bankCard}}
                                    </td>
                                </tr>
                                <tr>
                                    <th>
                                        <li>开户行</li>
                                    </th>
                                    <td>{{bankAdd}}</td>
                                </tr>
                                <tr>
                                    <th>
                                        <li>真实姓名</li>
                                    </th>
                                    <td>{{realName}}</td>
                                </tr>
                                <tr>
                                    <th>
                                        <li>手机号码</li>
                                    </th>
                                    <td>{{mobilePhone}}</td>
                                </tr>
                                </thead>
                            </table>
                        </div>
                    </div>
                    <div class="new_panel info_personal">
                        <div class="new_panel_top">个人信息
                            <a class="info_data_modify edit-btn"  v-if="showDetail" @click="editDetails()"><span class="icon icon_edit"></span>修改</a>
                            <a class="save save-btn"  v-if="!showDetail" @click="saveEdit()"><span class="icon icon_check"></span><span>保存</span></a>
                        </div>
                        <div class="new_panel_center print_data">
                            <table>
                                <thead>
                                <tr>
                                    <th>
                                        <li>微信</li>
                                    </th>
                                    <td v-if="!showDetail" class="before-edit">
                                        <input type="text" placeholder="请输入微信号" v-model="weChat">
                                        <!--<span class=" erro_text" >微信格式错误</span>-->
                                    </td>
                                    <td  v-if="showDetail" class="after-edit">{{weChat}}</td>
                                </tr>
                                <tr>
                                    <th>
                                        <li>QQ</li>
                                    </th>
                                    <td v-if="!showDetail" class="before-edit">
                                        <input  type="text"  placeholder="请输入QQ号" v-model="qq">
                                        <!--<span>qq格式错误</span>-->
                                    </td>
                                    <td v-if="showDetail" class="after-edit">{{qq}}</td>
                                </tr>
                                <tr>
                                    <th>
                                        <li>电子邮箱</li>
                                    </th>
                                    <td class="before-edit" v-if="!showDetail">
                                        <input  type="text"  placeholder="请输入邮箱地址" v-model="email">
                                        <!--<span class="errormsg erro_text" v-show="changeDetail.emailVali">邮箱格式错误</span>-->
                                    </td>
                                    <td v-if="showDetail" class="after-edit">{{email}}</td>
                                </tr>
                                </thead>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

        </div>
        <FooterNav></FooterNav>
        <!-- 登陸密碼 -->
        <div class="dropdown02 filter_dropdown_1 filter_dropdown" style="display:none;">
            <div class="play_area">
                <div class="password_area">
                    <form>
                        <fieldset v-if="show" >
                            <div class="form_g text">
                                <legend>原密码</legend>
                                <input type="password"  placeholder="请输入密码" v-model="oldPassword" class="oldPassword" @input="checkpassword(oldPassword,'oldPassword')">
                                <i class="icon icon_eye " @click="showPassword('eye1')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!show" >
                            <div class="form_g text">
                                <legend>原密码</legend>
                                <input type="text"  placeholder="请输入密码"  v-model="oldPassword" class="oldPassword" @input="checkpassword(oldPassword,'oldPassword')">
                                <i class="icon icon_eye active" @click="showPassword('act1')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="showC" >
                            <div class="form_g text">
                                <legend>新密码</legend>
                                <input type="password" placeholder="请输入新密码" v-model="newPassword"  class="newPassword" @input="checkpassword(newPassword,'newPassword')">
                                <i class="icon icon_eye " @click="showPassword('eye2')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!showC" >
                            <div class="form_g text">
                                <legend>新密码</legend>
                                <input type="text" placeholder="请输入新密码" v-model="newPassword"  class="newPassword" @input="checkpassword(newPassword,'newPassword')">
                                <i class="icon icon_eye active" @click="showPassword('act2')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="showB" >
                            <div class="form_g text">
                                <legend>确认密码</legend>
                                <input type="password" placeholder="请再次输入新密码" v-model="newPassword_confirm"  class="newPassword_confirm" @input="checkpassword(newPassword_confirm,'newPassword_confirm')">
                                <i class="icon icon_eye " @click="showPassword('eye3')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!showB" >
                            <div class="form_g text">
                                <legend>确认密码</legend>
                                <input type="text" placeholder="请再次输入新密码" v-model="newPassword_confirm"  class="newPassword_confirm" @input="checkpassword(newPassword_confirm,'newPassword_confirm')">
                                <i class="icon icon_eye active " @click="showPassword('act3')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                    </form>
                    <div>
                        <div class="cancel-btn btn_outlineb"><a class="new_btn cancel" href="javascript:;"><span>取消</span></a></div>
                        <div class="btn_blue02"><a class="new_btn ok" href="javascript:;"@click="submitChangePassword()" ><span>确定</span></a></div>
                    </div>
                </div>
            </div>
        </div>
        <!-- 支付密碼 -->
        <div class="dropdown filter_dropdown_2  filter_dropdown" style="display:none;">
            <div class="play_area">
                <div class="password_area">
                    <form>
                        <fieldset v-if="show" >
                            <div class="form_g text">
                                <legend>原密码</legend>
                                <input type="password"  placeholder="请输入取款密码" v-model="oldPayPassword" maxlength="4" class="oldPayPassword" @input="checkNum(oldPayPassword,'oldPayPassword')">
                                <i class="icon icon_eye " @click="showPassword('eye1')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!show" >
                            <div class="form_g text">
                                <legend>原密码</legend>
                                <input type="text"  placeholder="请输入取款密码"  v-model="oldPayPassword" class="oldPayPassword" maxlength="4" @input="checkNum(oldPayPassword,'oldPayPassword')">
                                <i class="icon icon_eye active" @click="showPassword('act1')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="showC" >
                            <div class="form_g text">
                                <legend>新密码</legend>
                                <input type="password" placeholder="请输入新取款密码" v-model="newPayPassword"  class="newPayPassword" maxlength="4" @input="checkNum(newPayPassword,'newPayPassword')">
                                <i class="icon icon_eye " @click="showPassword('eye2')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!showC" >
                            <div class="form_g text">
                                <legend>新密码</legend>
                                <input type="text" placeholder="请输入新取款密码" v-model="newPayPassword"  class="newPayPassword" maxlength="4" @input="checkNum(newPayPassword,'newPayPassword')">
                                <i class="icon icon_eye active" @click="showPassword('act2')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="showB" >
                            <div class="form_g text">
                                <legend>确认密码</legend>
                                <input type="password" placeholder="请再次输入新取款密码" v-model="newPayPassword_confirm"  class="newPayPassword_confirm" maxlength="4" @input="checkNum(newPayPassword_confirm,'newPayPassword_confirm')">
                                <i class="icon icon_eye " @click="showPassword('eye3')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                        <fieldset v-if="!showB" >
                            <div class="form_g text">
                                <legend>确认密码</legend>
                                <input type="text" placeholder="请再次输入新取款密码" v-model="newPayPassword_confirm"  class="newPayPassword_confirm" maxlength="4" @input="checkNum(newPayPassword_confirm,'newPayPassword_confirm')">
                                <i class="icon icon_eye active" @click="showPassword('act3')"></i>
                            </div>
                            <label class="error-message "></label>
                        </fieldset>
                    </form>
                    <div>
                        <div class="btn_outline cancel-btn"><a class="new_btn cancel" href="javascript:;"><span>取消</span></a></div>
                        <div class="btn_blue02"><a class="new_btn ok" href="javascript:;"@click="submitChangePayWord()"><span>确定</span></a></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="so-shade"></div>
        <AutoCloseDialog ref="autoCloseDialog" text=" " type="" />
    </div>
</template>

<script>
// import $ from "jquery";
import Mixin from '@/Mixin'
import AutoCloseDialog from '@/components/publicTemplate/AutoCloseDialog'
import FooterNav from '@/components/Footer'

export default {
  name: 'info_data',
  mixins:[Mixin],
  components: {
      AutoCloseDialog,
      FooterNav ,
  },
    data:function() {
        return {
             // 修改登录密码
            oldPassword:'',
            newPassword:'',
            newPassword_confirm:'',
            // 修改支付密码
            oldPayPassword:'',
            newPayPassword:'',
            newPayPassword_confirm:'',
           //客户个人信息
            loginName:'',
            weChat:'',
            qq:'',
            email:'',
            //用户银行信息
            realName:'',
            bankCard:'',
            bankName:'',
            bankAdd:'',
            mobilePhone:'',
            // 修改资料,
            showDetail:true,
            show:true,
            showC:true,
            showB:true,
            memberbalance:this.getCookie('membalance')
        }
    },
    created:function() {
        var _self = this;
//        _self.hasLogin = _self.ifLanded();
        _self.getUserBankInfo();
        _self.getUserInfo();


    },
    mounted:function() {
      $('html,body').css('overflow-y','scroll' );


        $('.filter_1').on('click',function () {
            $('.filter_dropdown_1 ').show() ;
        });
        $('.filter_2').on('click',function () {
            $('.filter_dropdown_2 ').show() ;
        });
        $('.cancel-btn').on('click',function () { /* .confirm-btn */
            $('.filter_dropdown ').hide() ;
        }) ;

  },
    methods: {
        // 获取用户银行信息
        getUserBankInfo: function() {
          var _self = this;
            $.ajax({
              type:'get',
              headers: { 'Authorization': 'bearer ' + _self.getAccessToken ,},
              dataType: 'json',
              url: _self.action.forseti + 'api/payment/memberBank',
              data: { },
              success: (res) => {

                   _self.realName=res.data.realName;
                   _self.bankCard=res.data.bankCard;
                   _self.bankName=res.data.bankName;
                   _self.bankAdd =res.data.bankAddress;
                   _self.mobilePhone =res.data.mobile

              },
              error: (err) =>{
              }
          })
//
      },
        //获取用户个人信息
        getUserInfo :function () {
            var _self=this;
            $.ajax({
                type: 'get',
                headers: {'Authorization': 'bearer ' + _self.getAccessToken,},
                dataType: 'json',
                url: _self.action.uaa + 'api/data/member/info',
                data: {},
                success: (res) => {
                    if(res.data){
                        _self.loginName=res.data.login;
                        _self.weChat  = res.data.wechat;
                        _self.qq      = res.data.qq;
                        _self.email   = res.data.email
                    }

                },
                error: (e)=>{

                }
            })
        },
        //修改登录密码
        submitChangePassword:function (){
            var _self=this;
             if(_self.oldPassword==''){
                 return false ;
             }
             if(_self.newPassword==''||_self.newPassword==_self.oldPassword){
                 _self.$refs.autoCloseDialog.open('原密码和新密码不能相同')
                 return false ;
             }
             if(_self.newPassword_confirm==''||_self.newPassword!=_self.newPassword_confirm){
                 _self.$refs.autoCloseDialog.open('两次新密码输入不一致')
              return false ;
             }
             var falg = $('.error-message').hasClass('red') ;  // 验证不通过，不允许提交
             if(falg){
               return false ;
             }
            var ChangePasswordData={
                oldPassword:_self.oldPassword,
                newPassword:_self.newPassword
               }
             $.ajax({
                 type:'post',
                 headers: { 'Authorization': 'bearer ' + _self.getAccessToken ,},
                 dataType: 'json',
                 url: _self.action.uaa + 'api/data/member/password',
                 data: ChangePasswordData,
                 success: (res) => {
                     if(res.err == 'SUCCESS'){
                         _self.$refs.autoCloseDialog.open('修改成功','','icon_check','d_check') ;
                         setTimeout(function(){
                             window.location = '/lobbyTemplate/info_data' ;
                         },2000)
                     }else{
                         _self.$refs.autoCloseDialog.open(res.msg) ;
                         return false
                     }

                 },
                 error: (err) =>{
                     _self.$refs.autoCloseDialog.open('请输入正确密码') ;
                 }
             })
      },
        //修改交易密码
        submitChangePayWord : function(){
          var _self=this;
            if(_self.oldPayPassword==''){
                  _self.$refs.autoCloseDialog.open('请输入原密码') ;
                   return false ;
              }else if(_self.oldPayPassword==_self.newPayPassword){
                _self.$refs.autoCloseDialog.open('原密码和新密码不能相同') ;
                return false ;
            }
           if(_self.newPayPassword ==''){
                 _self.$refs.autoCloseDialog.open('请输入新密码') ;
                 return false ;
              }
           if(_self.newPayPassword_confirm ==''){
              _self.$refs.autoCloseDialog.open('请再次输入新密码') ;
                  return false ;
              }else if(_self.newPayPassword!=_self.newPayPassword_confirm){
               _self.$refs.autoCloseDialog.open('请确认新密码是否一致') ;
                  return false ;
              }
            var  ChangePayWordData={
                 oldPassword:_self.oldPayPassword,
                 tradePassword:_self.newPayPassword
               }
          $.ajax({
              type:'post',
              headers: { 'Authorization': 'bearer ' + _self.getAccessToken ,},
              dataType: 'json',
              url: _self.action.forseti + 'api/pay/passwd',
              data:  ChangePayWordData,
              success: (res) => {
                  if(res.err == 'SUCCESS'){
                      _self.$refs.autoCloseDialog.open('修改成功','','icon_check','d_check') ;
                      setTimeout(function(){
                          window.location = '/lobbyTemplate/info_data' ;
                      },2000)
                  }else{
                      _self.$refs.autoCloseDialog.open(res.msg) ;
                     return false
                  }

              },
              error: (err) =>{
                  _self.$refs.autoCloseDialog.open('请输入正确密码') ;
              }
          })
      },
        //修改个人资料
        editDetails:function () {
            var _self=this;
            _self.showDetail=false

       } ,
        saveEdit :function () {
          var _self=this;
          if(_self.weChat==''||!_self.checkWechat(_self.weChat)){
               _self.$refs.autoCloseDialog.open('请输入正确微信号') ;
                return false
           }
          if(_self.qq==''||!_self.checkqq(_self.qq)){
               _self.$refs.autoCloseDialog.open('请输入正确QQ号') ;
               return false
          }
          if(_self.email==''||!_self.checkEmail(_self.email)){
              _self.$refs.autoCloseDialog.open('请输入正确的邮箱地址') ;
              return false
          }
          var EditData={
               wechat:_self.weChat,
               qq    :_self.qq,
               email :_self.email
          }
          $.ajax({
              type: 'post',
              headers: { 'Authorization': 'bearer ' + _self.getAccessToken ,},
              dataType: 'json',
              url: _self.action.uaa + 'api/data/member/chgInfo',
              data: EditData,
              success: (res) => {
                   if(res.err=='INPUT_ERR'){
                       _self.$refs.autoCloseDialog.open(res.msg) ;
                       return
                   }
                  _self.$refs.autoCloseDialog.open('修改成功','','icon_check','d_check') ;
                  setTimeout(function(){
                      window.location = '/lobbyTemplate/info_data' ;
                  },1000)

              },
              error: (err) =>{
                  _self.$refs.autoCloseDialog.open('请输入正确提款信息') ;
              }
          })
      },
        //点击显示密码
        showPassword :function(cla) {
            if(cla=="eye1"){
                this.show=false
            }else if(cla=="eye2"){
                this.showC=false
            }else if(cla=="eye3"){
                this.showB=false
            }else if(cla=="act1"){
                this.show=true;
            }else if(cla=="act2"){
                this.showC=true
            }else if(cla=="act3"){
                this.showB=true
            }
        }
}

}
</script>