<script lang="ts" setup>
const query = ref("");
function search(){
    @fetch()
}
</script>

<template>
    <form @submit.prevent="search">
        <input type="text" v-model="query">
        <button>Search</button>
    </form>
</template>

<style scoped></style>
