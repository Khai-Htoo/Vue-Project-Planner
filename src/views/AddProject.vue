<template>
    <form @submit.prevent="addProject">
       <div class="p-12">
          <h1 class="text-2xl font-bold mb-12 ">Add Task</h1>
        <label class="text-md font-bold text-slate-400 block">TASK TITLE</label>
        <input type="text" class="w-full border-b-2 p-2 outline-none text-xl mb-8 block" v-model="title"> 
        <label class="text-md font-bold  text-slate-400 block">TASK DETAIL</label>
        <input type="text" class="w-full w-full border-b-2 p-2 outline-none text-xl mb-5 block" v-model="detail">
        <button class=" bg-green-400 hover:bg-green-500 px-3 p-2 mt-5 rounded-md text-white font-bold">Add TASK</button>
       </div>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                title: "",
                detail:""
            }
        },
        methods: {
            addProject() {
               fetch('http://localhost:3000/projects',{
                method:"POST",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify({
                    title:this.title,
                    detail:this.detail,
                    complete:false
                })
               }).then(()=>{
                this.$router.push('/')
               }).catch((err)=>{
                 console.log(err);
               })
               
            }
        },
    }
</script>

<style scoped>

</style> 