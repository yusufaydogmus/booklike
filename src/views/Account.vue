<template>
    <app-header/>
    <div class="flex flex-row">
        <side-bar/>
        <!-- <component :is="$route.meta.componentName" :items="bookmarkList"/> -->
        <!-- <div class="socket">
            <input type="text" @keydown.enter="SEND_MESSAGE"/>
        </div> -->
    </div>
    <!-- <appBookmarkList v-if="bookmarkList.length>0" :items="bookmarkList"/>
    <div v-else> Bookmark Bulunmamaktadır</div> -->
</template>

<script>
import sideBar from "@/components/Account/sideBar";

export default {
    components: {
            sideBar
    },
    data(){
        return{
            bookmarkList:[],
        }
     },
    created(){
        this.$appAxios.get("/bookmarks?_expand=category&_expand=user").then(bookmark_list_response=>{ //expand edince category'i categories tablosunda arıyor ve sonuna categoryId ile arama yapıyor.
            console.log(bookmark_list_response)
            this.bookmarkList=bookmark_list_response?.data||[];
        })
    },
    // mounted(){
    //     this.$socket=io("http://localhost:2001") //bak burada bir socket sunucusu var 
    //     this.$socket.on("WELCOME_MESSAGE" , this.WELCOME_MESSAGE)
    // },
    methods:{
        // WELCOME_MESSAGE(data){
        //     console.log(data) 
        // },
        // SEND_MESSAGE(e){
        //     console.log(e.target.value)
        //     this.$socket.emit("SEND_MESSAGE", e.target.value)

        // }
    }
}
</script>