<template>
    <header>
        <img src="@/assets/images/logo.png" alt="Logo">
        <div class="search">
            <input
                type="text"
                placeholder="Film, Serie TV"
                v-model.trim="search"
            />
            <button @click="$emit('performSearch', search)"><i class="fas fa-search"></i></button>
        </div>
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

<style lang="scss" scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
    padding: 20px 50px;
    width: 100%;
    background: #141414;

    img {
        width: 150px;
    }

    .search {

        input {
            padding: 10px;
            width: 250px;
            height: 40px;
            background: #000;
            color: gray;
            border: 2px solid #fff;
            outline: 0;
        }

        button {
            width: 40px;
            height: 40px;
            background: #fff;
            border: 0;
        }
    }
}
</style>
