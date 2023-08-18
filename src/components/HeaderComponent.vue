<template>
    <div class="wrapper">
        <div class="header-wrap">
            <div>
                LOGO ALFA
            </div>
            <h2>
                Новости
            </h2>
        </div>
    </div>
</template>
<script>
export default {
    name: 'HeaderComponent',
    data() {
        return {};
    },
}
</script>
<style scoped>
.wrapper {
    height: 300px;

    background-image: url("../assets/img/top.jpg");
    background-position: center; 
    background-repeat: no-repeat; 
    background-size: cover; 
    margin-bottom: 30px;
}
.header-wrap {
    display: flex;
    flex-direction: column;
    height: 80%;
    justify-content: space-between;
    padding: 20px 0;
    margin-left: 10%;
}
</style>