<template>
    <footer id="Footer" ref="FooterEl"> <!-- @blur.capture="focusShow=false" -->
        <div class="cover" :class="{coverTop:focusShow,coverTopTop:showDescription}">
            <div class="errorValue" :class="{show:showError,top:focusShow,top101:showDescription}"
                 @click="[showError=false,$refs.text.focus()]">
                <p>ننوشتی ک 🙁</p>
                <span class="mdi mdi-close"></span>
            </div>
            <div class="preview" :class="{top:focusShow,top65:showDescription}"
                 @click="[$refs.text.focus(),showError=false]">
                <h4 @click="edit">موضوع : {{ title }}
                    <span class="mdi mdi-pencil" v-if="showDescription"></span>
                </h4>
                <p>توضیحات : {{ description }}</p>
                <span class="numberText">{{ numberText }} / {{ numberTextMax }}</span>
            </div>
        </div>
        <input type="text" placeholder="بنویس ..." v-model="text"
               @focus="[focusShow=true,showMenu=false,showMenuBox=false]" @input="textTitle"
               @keyup.enter="checkValid" ref="text" :maxlength="numberTextMax">
        <button class="mdi mdi-send btn" title="ارسال" @click="[checkValid(),showMenu=false,showMenuBox=false]"
                @focus="$refs.text.focus()"></button>
        <button class="mdi mdi-apps btn" title="بیشتر" @click="focusShow=false"
                @mousedown="showMenu=!showMenu" @mouseup="showMenuBox=!showMenuBox"></button>
        <div class="coverMenu" :class="{coverMenuTop:showMenu}">
            <transition
                enter-active-class="animate__animated animate__slideInLeft"
                leave-active-class="animate__animated animate__slideOutLeft animate__faster"
            >
                <div class="menuBox" v-show="showMenuBox">
                    <button class="item mdi mdi-github"></button>
                    <button class="item mdi mdi-github"></button>
                    <button class="item mdi mdi-github"></button>
                    <button class="item mdi mdi-github"></button>
                    <button class="item mdi mdi-github"></button>
                </div>
            </transition>
        </div>
    </footer>
</template>

<script>

export default {
    name: "Footer",
    data() {
        return {
            text: '',
            focusShow: false,
            title: '',
            showTitle: true,
            description: '',
            showDescription: false,
            showError: false,
            idPost: 0,
            isChecked: false,
            i: 1,
            list: [],
            numberText: 0,
            numberTextMax: 30,
            showMenu: false,
            showMenuBox: false,
        }
    },

    mounted() {
        document.body.addEventListener('click', (event) => {
            if (!(this.$refs.FooterEl === event.target || this.$refs.FooterEl.contains(event.path[0]))) {
                this.focusShow = false;
                this.showMenu = false;
                this.showMenuBox = false;
            }
        })
    },

    methods: {

        textTitle() {
            this.showError = false;
            this.numberText = this.text.length;
            if (this.showTitle) {
                this.title = this.text;
            } else if (!this.showTitle) {
                this.description = this.text;
            }
        },

        checkValid() {
            if (this.text == false) {
                this.showError = true;
                // this.$refs.text.focus()
            } else {
                this.showError = false;
                if (this.i === 1) {
                    this.showTitle = false;
                    this.title = this.text;
                    this.text = '';
                    this.i = 2;
                    this.showDescription = true;
                    this.idPost = this.generate(10000, 99999);
                    this.numberTextMax = 250;
                    this.numberText = 0;
                } else if (this.i === 2) {
                    this.showTitle = true;
                    this.list.push({
                        title: this.title,
                        description: this.description,
                        isChecked: this.isChecked,
                        idPost: this.idPost
                    });
                    this.$emit('changeList', this.list);
                    this.text = '';
                    this.title = '';
                    this.description = '';
                    this.i = 1;
                    this.showDescription = false;
                    this.numberTextMax = 30;
                    this.numberText = 0;
                }
            }
        },

        generate(min, max) {
            return Math.floor(Math.random() * (max - min) + min);
        },
        /*checkIdPost() {
            let id = this.generate(10000, 99999);
            // let listAppx = this.listApp;
            console.log(this.listApp);
            for (let list of this.listApp) {
                if (list.idPost === id ){
                    this.checkIdPost();
                }
            }
            // console.log(id);
        }*/


        edit() {

            let title = this.title;

            function editPopUp() {
                let i = prompt('ویرایش موضوع : ', title);
                if (i == false) {
                    alert('مقدار نمیتواند خالی باشه');
                    title = editPopUp();
                } else if (i == null) {
                    alert('کنسل شد');
                    return title;
                } else {
                    return i;
                }
                return title;
            }

            if (this.showDescription) {
                this.title = editPopUp();
            }
        },
    },


}
</script>

<style scoped>

</style>