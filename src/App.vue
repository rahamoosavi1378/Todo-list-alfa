<template>
    <div id="app">
        <div class="main" ref="rej">
            <div class="container">
                <Header></Header>
                <mainList :listApp="listApp"></mainList>
                <Footer @changeList="listApp = $event"></Footer>
            </div>
        </div>
    </div>
</template>

<script>

import Header from "@/components/header";
import MainList from "@/components/mainList";
import Footer from "@/components/footer";

export default {
    name: 'app',
    components: {Footer, MainList, Header},
    data() {
        return {
            listApp: [],
        }
    },
    methods: {
        loadFooter(){
            this.$refs.rej.addEventListener('click' , function(event){
                if (event.target.classList.contains('rejectEvent')) {
                    return false;
                }
                else{
                    alert('lol')
                }
            });
        },
    }
}
</script>

<style>

</style>
