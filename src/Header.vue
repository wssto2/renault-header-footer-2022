<template>
    <div class="plugin-helios-header-footer" data-fplugin="local-data">
                
        <div id="helios-header" class="helios-header helios-special-elements">
            <nav class="top-nav">
                
                <ul class="module-container" data-fplugin="expand-menu" data-fopts="{&quot;triggerSelector&quot;:&quot;.dropdown&quot;, &quot;containerSelector&quot;:&quot;.expand-container&quot;, &quot;grouped&quot; : true}">
                    
                    <li v-for="(topMenuItem, topMenuIndex) in topNavigation" :key="topMenuIndex" class="padding-left-5">
                        <a :data-tracking-name="topNavIndexClass" data-tracking-location="Menu top navigation" class=" gtm-button " :href="topMenuItem.url" title="" target="_self" rel="nofollow noreferrer">
                            <span v-if="topMenuItem.icon === 'icon-search'" class="search-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30" width="16" height="16" fill="#fff" class="e11fteez1 header-1n0oa5t e3bhxjg0"><path d="M13.07 6.26c-3.69 0-6.81 2.73-6.81 6.691 0 4.02 3.15 7.05 6.93 7.05 3.721 0 6.811-2.76 6.811-6.69 0-4.05-3.12-7.05-6.93-7.05m8.19 7.02c0 2.01-.69 3.75-1.83 5.13l5.85 5.851-.87.9-5.88-5.88c-1.44 1.26-3.33 1.98-5.37 1.98C8.72 21.262 5 17.66 5 12.98 5 8.361 8.72 5 13.1 5c4.53 0 8.16 3.511 8.16 8.281"></path></svg>
                            </span>
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
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30" width="20" height="20" fill="#fff"><path d="M28.75 2.5H1.25a1.25 1.25 0 0 0 0 2.5h27.5a1.25 1.25 0 0 0 0-2.5zM1.25 16.25h17.5a1.25 1.25 0 0 0 0-2.5H1.25a1.25 1.25 0 0 0 0 2.5zM23.75 25H1.25a1.25 1.25 0 0 0 0 2.5h22.5a1.25 1.25 0 0 0 0-2.5z"></path></svg>
                            </div>
                            

                            
                            <nav class="header-part menu hidden-xs">
                    
                                <ul class="main-navigation">
                                    <li class="visible-xs visible-sm">
                                        <a class="header-icon header-icon-home" :href="basicInformation.site_url"><span>Renault</span></a>
                                    </li>
                                    <DropdownLink 
                                        v-for="(navigationItem, itemIndex) in mainNavigation" 
                                        :key="itemIndex" 
                                        :item="navigationItem"
                                        :itemIndex="itemIndex"
                                        :isActive="dropdownActive === itemIndex"
                                        @toggleDropdown="toggleDropdown"
                                    />
                                </ul>
                            </nav>
                
                        </header>

                        <nav  :class="['mobile-menu', { 'is-active' : mobileDropdown}]" :style="mobileDropdown ? 'display: flex;' : 'display: none;'">
                            <div class="close-button-container">
                                <div class="close-button menu-trigger" @click="toggleMobileDropdown" data-phf-ico-active-after=""></div>
                            </div>
                            <div class="mobile-menu-container">
                                <div class="mobile-menu-heading">
                                    <span>{{ basicInformation.site_title }}</span>
                                </div>
                                <div>
                                    <MobileDropdown 
                                        :navigation="mainNavigation"
                                    />
                                </div>
                                <div class="mobile-menu-search">
                                    <a href="https://www.renault.hr/searchResult.html">
                                        <span><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30" width="16" height="16" fill="#fff" class="e11fteez1 header-1n0oa5t e3bhxjg0"><path d="M13.07 6.26c-3.69 0-6.81 2.73-6.81 6.691 0 4.02 3.15 7.05 6.93 7.05 3.721 0 6.811-2.76 6.811-6.69 0-4.05-3.12-7.05-6.93-7.05m8.19 7.02c0 2.01-.69 3.75-1.83 5.13l5.85 5.851-.87.9-5.88-5.88c-1.44 1.26-3.33 1.98-5.37 1.98C8.72 21.262 5 17.66 5 12.98 5 8.361 8.72 5 13.1 5c4.53 0 8.16 3.511 8.16 8.281"></path></svg></span>
                                        <span class="title">traži</span>
                                    </a>
                                </div>
                                <div class="mobile-menu-bottom-links">
                                    <ul>
                                        <li v-for="(topMenuItem, topMenuIndex) in filteredTopNavigation" :key="topMenuIndex" class="padding-left-5">
                                            <a :data-tracking-name="topNavIndexClass" data-tracking-location="Menu top navigation" class=" gtm-button " :href="topMenuItem.url" title="" target="_self" rel="nofollow noreferrer">
                                                <span v-if="topMenuItem.icon === 'icon-search'" class="search-icon">
                                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30" width="16" height="16" fill="#fff" class="e11fteez1 header-1n0oa5t e3bhxjg0"><path d="M13.07 6.26c-3.69 0-6.81 2.73-6.81 6.691 0 4.02 3.15 7.05 6.93 7.05 3.721 0 6.811-2.76 6.811-6.69 0-4.05-3.12-7.05-6.93-7.05m8.19 7.02c0 2.01-.69 3.75-1.83 5.13l5.85 5.851-.87.9-5.88-5.88c-1.44 1.26-3.33 1.98-5.37 1.98C8.72 21.262 5 17.66 5 12.98 5 8.361 8.72 5 13.1 5c4.53 0 8.16 3.511 8.16 8.281"></path></svg>
                                                </span>
                                                <span><span v-if="topMenuItem.meta.bold" :style="topMenuItem.meta.yellow ? 'color: #000 !important; background-color: #efdf00;' : ''"><b>{{ topMenuItem.title }}</b></span><span v-else :style="topMenuItem.meta.yellow ? 'color: #000 !important; background-color: #efdf00;' : ''">{{ topMenuItem.title }}</span></span>
                                            </a>
                                        </li>
                                    </ul>
                                </div>
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

            <Dropdown 
                v-for="(navigationItem, itemIndex) in mainNavigation" 
                :key="itemIndex" 
                :item="navigationItem"
                :itemIndex="itemIndex"
                :dropdownActiveType="dropdownActive"
            />
        </div>

</template>

<script>
    import axios from 'axios';
    import Dropdown from "@/components/Dropdown";
    import DropdownLink from "@/components/DropdownLink"
    import MobileDropdown from "@/components/MobileDropdown"

    export default {
        components: { Dropdown, DropdownLink, MobileDropdown },
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
                mainNavigation: [],
                dropdownActive: null
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
            },

            filteredTopNavigation() {
                return this.topNavigation.slice(0, -1);
            }
        },
        methods: {
            toggleDropdown(index) {
                this.dropdownActive = this.dropdownActive === index ? null : index;
            },

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
    .plugin-helios-header-footer {
        position: relative;
    }
</style>
