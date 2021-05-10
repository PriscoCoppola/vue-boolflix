<template>
    <header>
        <input 
            type="text" 
            placeholder="Inserisci film" 
            v-model="search"
        />
        <button @click="$emit('performSearch', search)">Search</button>
    </header>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            search: '',
        }
    }
};
</script>

<style lang="scss" scoped></style>
