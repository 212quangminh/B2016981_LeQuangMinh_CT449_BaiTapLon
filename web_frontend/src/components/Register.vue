<template>
   <div class="container">
      <div class="d-flex justify-content-center h-100">
         <div class="card shadow-lg p-3 mb-5 bg-body rounded">
            <div class="card-header text-center">
               <h3>Đăng ký tài khoản</h3>
            </div>
            <div class="card-body">
               <form @submit.prevent="register()">
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text">
                           <i class="fa-solid fa-user"></i>
                        </span>
                     </div>
                     <input
                        type="text"
                        class="form-control"
                        placeholder="Họ và tên"
                        @blur="validate()"
                        v-model="user.name"
                        :class="{ 'is-invalid': errors.name }"
                     />
                     <div class="invalid-feedback" v-if="errors.name">
                        {{ errors.name }}
                     </div>
                  </div>
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text">
                           <i class="fa-solid fa-envelope"></i>
                        </span>
                     </div>
                     <input
                        type="email"
                        class="form-control"
                        placeholder="Email"
                        @blur="validate()"
                        v-model="user.email"
                        :class="{ 'is-invalid': errors.email }"
                     />
                     <div class="invalid-feedback" v-if="errors.email">
                        {{ errors.email }}
                     </div>
                  </div>
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text">
                           <i class="fas fa-key"></i>
                        </span>
                     </div>
                     <input
                        type="password"
                        class="form-control"
                        placeholder="Mật khẩu"
                        @blur="validate()"
                        v-model="user.password"
                        :class="{ 'is-invalid': errors.password }"
                     />
                     <div class="invalid-feedback" v-if="errors.password">
                        {{ errors.password }}
                     </div>
                  </div>
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text">
                           <i class="fa-solid fa-shield"></i>
                        </span>
                     </div>
                     <input
                        type="password"
                        class="form-control"
                        placeholder="Nhập lại mật khẩu"
                        @blur="validate()"
                        v-model="user.repassword"
                        :class="{ 'is-invalid': errors.repassword }"
                     />
                     <div class="invalid-feedback" v-if="errors.repassword">
                        {{ errors.repassword }}
                     </div>
                  </div>
                  <div class="form-group">
                     <input
                        type="submit"
                        value="Đăng ký"
                        class="btn login_btn"
                     />
                  </div>
               </form>
            </div>
            <div class="card-footer">
               <div class="d-flex justify-content-center links">
                  <p>
                     Đăng nhập ngay!
                     <router-link to="/login"><b>ĐĂNG NHẬP</b></router-link>
                  </p>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
import UserService from "../services/user.service";

export default {
   data() {
      return {
         errors: {
            name: "",
            email: "",
            password: "",
            repassword: "",
         },
         user: {
            name: "",
            email: "",
            password: "",
            repassword: "",
         },
      };
   },
   methods: {
      validate() {
         let isValid = true;

         this.errors = {
            name: "",
            email: "",
            password: "",
            repassword: "",
         };

         if (!this.user.name) {
            this.errors.name = "Họ và tên là bắt buộc";
            isValid = false;
         }
         if (!this.user.email) {
            this.errors.email = "Email là bắt buộc";
            isValid = false;
         }
         if (!this.user.password) {
            this.errors.password = "Mật khẩu là bắt buộc";
            isValid = false;
         }
         if (this.user.repassword != this.user.password) {
            this.errors.repassword = "Mật khẩu chưa đúng";
            isValid = false;
         }
         return isValid;
      },
      async register() {
         if (this.validate()) {
            try {
               await UserService.create(this.user);
               alert(
                  `Chúc mừng ${this.user.name.toUpperCase()} !!! Bạn đã đăng ký tài khoản thành công!`
               );
            } catch (error) {
               console.log(error);
            }
         }
      },
   },
};
</script>

<style scoped>
.container {

   padding-top: 80px;
   padding-bottom: 100px;
   margin-top: 10px;
}
.d-flex{
   background-color: #E38B29;
   /* color: aliceblue; */
}
.container{
   background-color: #E38B29;
}
.card {
   height: 520px;
   margin-top: auto;
   margin-bottom: auto;
   width: 400px;
   /* border: 1px solid #E38B29; */
   /* border-radius: 10px; */

}
.form-control{
	font-size: 16px;
	color: orange;
	border: none; 
	border-bottom: 1px solid black;	
	outline: none;
	background:transparent ;
}
.social_icon span {
   font-size: 60px;
   margin-left: 10px;
   color: #E38B29;
}
.social_icon span:hover {
   color: white;
   cursor: pointer;
}
.card-header h3 {
   color: #E38B29;
}
.card-header{
   background-color: white;
   border-radius: 10px;
}
.social_icon {
   position: absolute;
   right: 20px;
   top: -45px;
}
.input-group-prepend span {
   width: 50px;
   background-color: white;
   color: #E38B29;
   border: 0 !important;
}
input:focus {
   outline: 0 0 0 0 !important;
   box-shadow: 0 0 0 0 !important;
}
.login_btn {
   color: #E38B29;
   border-radius: 20px;
   border: 1px solid #E38B29;
   width: 50%;
   margin-left: 25%;
}
.login_btn:hover {
   color: white;
   background-color: #E38B29;
}
.links {
   color: white;
}
.card-footer{
   background-color: white;
   border-radius: 10px;
}
.links {
   color: #E38B29;
   background-color: white;
}
.links a {
   margin-left: 4px;
   text-decoration: none;
   color:#E38B29;
}
</style>
