<template>
    <div class=" bg-slate-200 mb-3 p-8 mt-5 flex justify-between rounded-l-lg"  :class="{complete:project.complete,not:!project.complete}" @click.self="detail = !detail">
        <div class="">
            <h1 class=" text-xl font-bold text-purple-900 mb-3">{{project.title}}</h1>
            <p v-if="detail">{{project.detail}}</p>
        </div>
        <div class="flex gap-2">
            <router-link :to="{name:'EditProject',params:{id:project.id}}">
                 <div class="" >
                 <i class="fa-solid fa-pen-to-square text-2xl text-slate-800 mb-2 cursor-pointer"></i>
            </div>
            </router-link>
             <lord-icon
                @click="completeProject"
                src="https://cdn.lordicon.com/egiwmiit.json"
                trigger="hover"
                class="cursor-pointer"
                colors="primary:black"
                style="width:30px;height:30px">
            </lord-icon>
            <lord-icon
                @click="deleteProject"
                src="https://cdn.lordicon.com/kfzfxczd.json"
                trigger="hover"
                class="cursor-pointer"
                colors="primary:black"
                style="width:30px;height:30px">
            </lord-icon>
       
        </div>
    </div>
</template>

<script>
    export default {
        props:['project'],
        data() {
            return {
                detail: false,
                api:'http://localhost:3000/projects/'
            }
        },
        methods: {
            deleteProject() {
                let deletePro = this.api+this.project.id
               fetch(deletePro,{method:"DELETE"})
               .then(()=>{
                  this.$emit("delete",this.project.id)
               }).catch((err)=>{
                  console.log(err);
               })
            },
            completeProject(){
                let completeRoute = this.api+this.project.id;
                fetch(completeRoute,{
                    method:"PATCH",
                    headers:{
                        "Content-Type":"application/json"
                    },
                    body:JSON.stringify({
                        complete:!this.project.complete
                    })
                    }).then(()=>{
                        this.$emit("complete",this.project.id)
                    })
            },
        },

    }
</script>

<style  scoped>
.not{
    border-left: 6px solid crimson;

}
.complete{
        border-left: 6px solid green;
}
</style>