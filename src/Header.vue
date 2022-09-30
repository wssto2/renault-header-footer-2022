<template>
    <div class="plugin-helios-header-footer" data-fplugin="local-data">
                
        <div id="helios-header" class="helios-header helios-special-elements">
            <nav class="top-nav">
                
                <ul class="module-container" data-fplugin="expand-menu" data-fopts="{&quot;triggerSelector&quot;:&quot;.dropdown&quot;, &quot;containerSelector&quot;:&quot;.expand-container&quot;, &quot;grouped&quot; : true}">
                    
                    <li v-for="(topMenuItem, topMenuIndex) in topNavigation" :key="topMenuIndex" class="padding-left-5">
                        <a :data-tracking-name="topNavIndexClass" data-tracking-location="Menu top navigation" class=" gtm-button " :href="topMenuItem.url" title="" target="_self" rel="nofollow noreferrer">
                            <span><span v-if="topMenuItem.meta.bold" :style="topMenuItem.meta.yellow ? 'color: #000 !important; background-color: #efdf00;' : ''"><b>{{ topMenuItem.title }}</b></span><span v-else :style="topMenuItem.meta.yellow ? 'color: #000 !important; background-color: #efdf00;' : ''">{{ topMenuItem.title }}</span></span>
                        </a>
                    </li>
                    
                </ul>
            </nav>
    
            <div data-fplugin="picture-lazy-loading" data-fopts="{&quot;imagesLoadingTrigger&quot;:&quot;.expand-box&quot;, &quot;eventToLoadImages&quot;:&quot;mouseenter&quot;, &quot;event&quot;: &quot;loadOnEvent&quot;}">
                <div data-fplugin="expand-menu" data-fopts="{&quot;triggerSelector&quot;:&quot;.dropdown&quot;, &quot;containerSelector&quot;:&quot;.expand-container&quot;, &quot;grouped&quot; : true}">
                    <div class="page-header--helios" data-fplugin="menu">
                        <header class="module-container">
                            <div class="header-part brand-logo">
                                <a :href="basicInformation.site_url" :title="basicInformation.site_title">
                                    <img src="https://unpkg.com/@wssto2/rv-renault-header-footer-cg-bih-new-main/dist/img/renault-logo.svg" alt="Renault Logo">
                                </a>
                            </div>

                            <div class="header-part menu-trigger ico-before-menu" @click="toggleMobileDropdown">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="20"><defs><filter id="a"><feColorMatrix in="SourceGraphic" values="0 0 0 0 1.000000 0 0 0 0 1.000000 0 0 0 0 1.000000 0 0 0 1.000000 0"/></filter></defs><g filter="url(#a)" transform="translate(-280 -20)"><g transform="translate(280 20)"><rect width="24" height="2" rx="1"/><rect width="16" height="2" y="9" rx="1"/><rect width="20" height="2" y="18" rx="1"/></g></g></svg>
                            </div>
                            

                            
                            <nav class="header-part menu hidden-xs">
                    
                                <ul class="main-navigation">
                                    <li class="visible-xs visible-sm">
                                        <a class="header-icon header-icon-home" :href="basicInformation.site_url"><span>Renault</span></a>
                                    </li>
                                    <Dropdown 
                                        v-for="(navigationItem, itemIndex) in mainNavigation" 
                                        :key="itemIndex" 
                                        :item="navigationItem"
                                        :itemIndex="itemIndex"
                                         @showModal="toggleCarCategory"
                                        />
                                    
                                </ul>
                            </nav>
                
                        </header>

            
                        <nav :class="['mobile-menu', { 'is-active' : mobileDropdown}]" :style="mobileDropdown ? 'display: block;' : 'display: none;'">
                            <div class="close-button menu-trigger" @click="toggleMobileDropdown" data-phf-ico-active-after=""></div>
                
                                <ul class="main-navigation">
                                    <li class="visible-xs visible-sm">
                                        <a class="header-icon header-icon-home" :href="basicInformation.site_url"><span>Renault</span></a>
                                    </li>
                                    
                                    <Dropdown 
                                        v-for="(navigationItem, itemIndex) in mainNavigation" 
                                        :key="itemIndex" 
                                        :item="navigationItem"
                                        :itemIndex="itemIndex"
                                         @showModal="toggleCarCategory"
                                        />
                                    
                                </ul>
            
                                <div class="navigation-top-mobile">
                    
                                    <ul class="module-container">
                                        
                                        <li v-for="(topMenuItem, topMenuIndex) in topNavigation" :key="topMenuIndex" class="padding-left-5">
                                            <a :data-tracking-name="topNavIndexClass" data-tracking-location="Menu top navigation" class=" gtm-button " :href="topMenuItem.url" title="" target="_self" rel="nofollow noreferrer">
                                                <span><span>{{ topMenuItem.title }}</span></span>
                                            </a>
                                        </li>
                                      
                                    </ul>
                                </div>
                            </nav>
                            <div class="nav-mask"></div>
            
                        </div>

                        <nav :class="['menu-popup', { 'is-active' : (Number.isInteger(activeCarCategory)) }]" style="min-height: 938px;">
                            <div class="menu-popup_close">Zatvori</div>
                            <div class="menu-popup_inner" v-if="mainNavFirst != 0">

                                <div v-show="activeCarCategory === carPickerIndex" v-for="(carPicker, carPickerIndex) in mainNavFirst" :key="carPickerIndex" class="menu-popup_vehicles-container  is-active" data-popup="595468798" style="left: 327px;">
                                    
                                    <a :href="carPicker.url" class="menu-popup_vehicle-block menu-popup_range">
                                        <span class="menu-popup_icon" :data-phf-ico-after="carPicker.icon"></span>
                                        <span class="menu-popup_vehicle-name">{{carPicker.title}}</span>
                                    </a>
                                    <a  v-for="(carElement, carElementIndex) in carPicker.children" :key="carElementIndex" :href="carElement.url" target="_self" class="menu-popup_vehicle-block">
                                        <span class="menu-popup_img">
                                            <img :src="carElement.icon">
                                        </span>
                                        <span class="menu-popup_vehicle-name">{{carElement.title}}</span>
                                    </a>
                                </div>                                
                                
                            </div>
                        </nav>
                        <div class="menu-popup_mask"></div>
                    </div>
    
                    <nav class="progress-nav helios-special-elements">
    
                    </nav>
                </div>
            </div>
        </div>

</template>

<script>
    import axios from 'axios';
    import Dropdown from "@/components/Dropdown";

    export default {
        components: { Dropdown },
        name: 'Header',
        created() {
            if ("HEADER_FOOTER_SETTINGS" in window) {
                this.fetchNavigation(window.HEADER_FOOTER_SETTINGS.apiUri);
            } else {
                if (this.url) {
                    this.fetchNavigation(this.url);
                }
            }

            window.addEventListener('click', this.del)
        },
        data() {
            return {
                logo: require("@/assets/images/renault-logo.svg"),
                expanded: false,
                mobileDropdown: false,
                activeCarCategory: null,
                basicInformation: [],
                topNavigation: [],                 
                mainNavigation: []
            }
        },
        beforeDestroy() {
            window.removeEventListener('click', this.del)
        },

        computed: {
            topNavIndexClass(){
                return true
            },
            
            mainNavFirst() {
                return  this.mainNavigation && this.mainNavigation[0] && this.mainNavigation[0].children;
            }
        },
        methods: {
            fetchNavigation(apiUri) {
                axios.get(apiUri)
                    .then((response) => {
                        this.basicInformation = response.data;
                        this.topNavigation = response.data.top_navigation.schema;
                        this.mainNavigation = response.data.main_navigation.schema;
                    })
            },
            toggleMobileDropdown(){
                this.mobileDropdown = !this.mobileDropdown
            },
            toggleCarCategory(index){
                console.log(index);
                if(this.activeCarCategory === index) {
                    this.activeCarCategory = null
                } else {
                    this.activeCarCategory = index
                }
                if(index === null) {
                    this.activeCarCategory = null
                }
                
            },
            del(e) {
                if(! this.$el.contains(e.target)){
                    this.mobileDropdown = false
                }
            }
        }
    }
</script>

<style scoped>
    @import './assets/css/main.css';

    @font-face{
        font-family:"readBeta2 sans-serif";
        font-weight:400;
        font-display:swap;
        src:url(./assets/fonts/readBeta2-Light.woff2) format("woff2")
    }
    @font-face{
        font-family:"readBeta2 sans-serif";
        font-weight:700;
        font-display:swap;
        src:url(./assets/fonts/readBeta2-Medium.woff2) format("woff2")
    }
    @font-face{
        font-family:"RenaultLife";
        font-weight:300;
        font-display:swap;
        src:url(./assets/fonts/RenaultLifeWeb-Light.woff) format("woff")
    }
    @font-face{
        font-family:"RenaultLife";
        font-weight:400;
        font-display:swap;
        src:url(./assets/fonts/RenaultLifeWeb-Regular.woff) format("woff")
    }
    @font-face{
        font-family:"RenaultLife";
        font-weight:700;
        font-display:swap;
        src:url(./assets/fonts/RenaultLifeWeb-Bold.woff) format("woff")
    }
    @font-face{
        font-family:NouvelR-Regular;
        font-weight:400;
        font-display:swap;
        src:url(./assets/fonts/NouvelR-Regular.woff2) format("woff2")
    }
    @font-face{
        font-family:NouvelR-Bold;
        font-weight:700;
        font-display:swap;
        src:url(./assets/fonts/NouvelR-Bold.woff2) format("woff2")
    }
    @font-face{
        font-family:Pictos;
        font-style: normal;
        font-weight: 400;
        src:url(./assets/fonts/PictosCompleteXXI-Regular.woff) format("woff")
    }
</style>
