<template>
  <div class="fixed top-0 left-0 w-full bg-white flex justify-between  shadow-lg z-50">
    <div class="w-[200px]   px-6 py-3 flex items-center justify-end"> 
      <div class="relative">
        <select
          v-model="locale"
          class="appearance-none bg-white border border-blue-200 text-gray-700 py-2   px-4 pr-8 hover:outline-none rounded-md focus:outline-none focus:ring-2 focus:ring-blue-100 cursor-pointer"
        >
          <option value="uz">🇺🇿 Uzbek</option>
          <option value="en">🇬🇧 English</option>
        </select>
        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
          <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg"
               viewBox="0 0 20 20">
            <path d="M5.516 7.548l4.484 4.482 4.484-4.482L16 9l-6 6-6-6z"/>
          </svg>
        </div>
      </div>
    </div>
    <div class=" w-[150px] items-center flex justify-between mr-[20px]">  
      <a v-if="!isTokenExist" href="https://eu-central-1bjxkrimqu.auth.eu-central-1.amazoncognito.com/login?client_id=79tlitdlu0haogq1201dt31kae&response_type=code&scope=openid+email+phone&redirect_uri=http://localhost:5173/">Login</a>
      <a v-if="!isTokenExist" href="https://eu-central-1bjxkrimqu.auth.eu-central-1.amazoncognito.com/login?client_id=79tlitdlu0haogq1201dt31kae&response_type=code&scope=openid+email+phone&redirect_uri=http://localhost:5173/">Sign up</a> 
      <a
        v-if="isTokenExist" 
        href="#" 
        @click="LogOut()"

        >Log out</a>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted} from "vue"
import { useI18n } from 'vue-i18n'
const { locale } = useI18n()

const isTokenExist = ref(false)
const paramsFromUrl = new URLSearchParams(window.location.search);
const authCode = paramsFromUrl.get("code");
 


async function exchangeAuthToJWT(authToken:string){
  if (authToken) {
  
  const tokenUrl = "https://eu-central-1bjxkrimqu.auth.eu-central-1.amazoncognito.com/oauth2/token";
 
  const bodyParams = new URLSearchParams();
  bodyParams.append("grant_type", "authorization_code");  // fixed value
  bodyParams.append("client_id", "79tlitdlu0haogq1201dt31kae");
  bodyParams.append("code",authToken);                    
  bodyParams.append("redirect_uri", "http://localhost:5173/");
   
  try{
     const res = await fetch(tokenUrl,{
      method: 'POST',
      headers:{
        "Content-Type": "application/x-www-form-urlencoded"       
      },
      body: bodyParams
     })

     const data = await res.json()
      
     localStorage.setItem('AccessToken',data.access_token)
     localStorage.setItem('RefreshToken',data.refresh_token)

     isTokenExist.value = true

     console.log(data)
  }catch(err){
    console.log(err)
  } 

} else {
  console.log("No authorization code in URL.");
}
}

function LogOut(){
  isTokenExist.value = false
  localStorage.removeItem('AccessToken')
  localStorage.removeItem('RefreshToken')
}

onMounted(()=> {
  exchangeAuthToJWT(authCode!)
})
</script>

<style scoped>

select:hover {
  border-color: #2563eb;  
}
</style>