<template>
    <div>
        <button @click="filter('all')" class="bg-slate-200 text-lg font-bold px-3 p-1" :class="{active : current === 'all'}" >All</button>
        <button @click="filter('Complete')" class="bg-slate-200 text-lg font-bold px-3 p-1" :class="{active : current === 'Complete'}">Complete</button>
        <button @click="filter('Ongoing')" class="bg-slate-200 text-lg font-bold px-3 p-1" :class="{active : current === 'Ongoing'}">Ongoing</button>
    </div>
</template>

<script>
    export default {
        props:["current"],
        methods: {
            filter(value) {
                this.$emit('filterValue',value)
            }
        },
    }
</script>

<style  scoped>
.active{
 color: #00ce89;
}

</style>