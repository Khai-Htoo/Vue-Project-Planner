<template>
    <div>
      <form @submit.prevent="editProject">
       <div class="p-12">
          <h1 class="text-2xl font-bold mb-12 ">Edit Project {{id}}</h1>
        <label class="text-md font-bold text-slate-400 block">PROJECT TITLE</label>
        <input type="text" class="w-full border-b-2 p-2 outline-none text-xl mb-8 block" v-model="title"> 
        <label class="text-md font-bold  text-slate-400 block">PROJECT DETAIL</label>
        <input type="text" class="w-full w-full border-b-2 p-2 outline-none text-xl mb-5 block" v-model="detail">
        <button @click="editProject" class=" bg-green-400 hover:bg-green-500 px-3 p-2 mt-5 rounded-md text-white font-bold">Edit Project</button>
       </div>
    </form>
    </div>
</template>

<script>
    export default {
        props:['id'],
        data() {
            return {
                title: "",
                detail:""
            }
        },
        methods: {
            editProject() {
                fetch('http://localhost:3000/projects/'+this.id,{
                    method:'PATCH',
                    headers:{
                        "Content-Type":"application/json"
                    },
                    body:JSON.stringify({
                       title : this.title,
                       detail : this.detail
                    })
                    })
                .then(()=>{
                    this.$router.push('/')
                }).catch((err)=>{
                    console.log(err);
                })
            }
        },
        mounted () {
            fetch('http://localhost:3000/projects/'+this.id).then((response)=>{
                return response.json()
            }).then((data)=>{
                this.title =data.title,
                this.detail= data.detail
            }).catch((err)=>{
                console.log(err);
            })
        },
     
    }
</script>

<style lang="scss" scoped>

</style>