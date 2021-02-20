<template>
    <header id="header">
        <img src="@/assets/header-bg-4.jpg" alt="header-bg">
        <span class="data">تاریخ امروز</span>
        <button class="mdi mdi-refresh refresh"></button>
    </header>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            listImg: ['header-bg-1.jpg', 'header-bg-2.jpg', 'header-bg-3.jpg', 'header-bg-4.jpg'],
        }
    },
}
</script>

<style scoped>

</style>