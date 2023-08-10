<template>
    <div class="login_register_container">
      <h3 class="text-2xl text-center mb-3">Kayıt Ol</h3>
      <input v-model="userData.fullname" type="text" placeholder="Tam Ad" class="input mb-3" />
      <input v-model="userData.username" type="text" placeholder="Kullanıcı Adı" class="input mb-3" />
      <input v-model="userData.password" type="password" placeholder="Şifre" class="input mb-3" />
      <button class="default-button" @click="onSave">Kayıt ol</button>
      <span class="text-center mt-3 text-sm">
        Zaten Üyeyim,
        <router-link :to="{name:'LoginPage'}" class="text-red-900 hover:text-black">
        Giriş Yap
        </router-link>
      </span>
    </div>
</template>

<script>
import CryptoJS from "crypto-js"
export default{
  data(){
    return{
      userData:{
        username:null,
        fullname:null,
        password:null
      }
    }
  },
  methods:{
      onSave(){
        //const password=this.userData.password;
        //const key="booklike123Q456"
        //const cryptedPassword=CryptoJS.AES.encrypt(password,key).toString();
        //direkt 
        //const password =CryptoJS.AES.encrypt(this.userData.password,this.$store.getters._saltKey).toString();
        
        
        //const password =CryptoJS.SHA256(this.userData.password).toString(); 
        
        const password =CryptoJS.HmacSHA1(this.userData.password,this.$store.getters._saltKey).toString(); 

        


        console.log(password);
        /*
        const decryptedPassword=CryptoJS.AES.decrypt(cryptedPassword,key).toString(CryptoJS.enc.Utf8);
  
        console.log(decryptedPassword);
        // console.log(this.userData);
        */
        this.$appAxios.post("users",{...this.userData,password  /* :cryptedPassword*/}).then(registered_user_response=>{ //sen users'a appAxios ile  post isteği at obje olarak userData'yı gönder fakat password'u ez ve gönder
           console.log('registered_user_response', registered_user_response)
            this.$router.push({name:"HomePage"})
        })
      }
    } 
}
</script>