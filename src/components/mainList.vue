<template>
    <section>
        <div class="listBox" v-for="(item,index) in listApp" :key="index">
            <div class="number" v-text="++index"></div>
            <div class="list">
                <h4 v-text="item.title"></h4>
                <p v-text="item.description"></p>
                <span class="mdi mdi-close"></span>
                <span class="idPost">#{{item.idPost}}</span>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "mainList",
    props: ['listApp'],
}
</script>

<style scoped>

</style>