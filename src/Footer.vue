<template>
    <div class="plugin-helios-header-footer">         
        <div id="helios-footer" class="helios-footer helios-special-elements">
            <div class="page-footer">
                <footer>
                    <div class="module-container">
                        <div class="container-fluid">
                            <ul v-if="mainFooter != 0 || socialNavigation != 0" class="row footer-menu" data-fplugin="expand-content" data-fres="[&quot;xs&quot;]" data-fopts="{&quot;expandTriggerClass&quot;: &quot;open&quot;, &quot;collapsedDisplay&quot; : &quot;&quot;, &quot;grouped&quot; : &quot;true&quot;, &quot;collapsedDisplay&quot; : &quot;&quot;}">
                                <li v-for="(item, itemIndex) in mainFooter" :key="itemIndex" class="col-xs-12 col-sm-4 col-md-3 expand-box">
                                    <div :class="['menu-group-name','trigger', {'open': isVisible(itemIndex)}]" @click.prevent="toggle(itemIndex)">{{ item.title }}</div>
                                    
                                    <ul :class="['footer-menu', 'container-show', {'displayBlock' :  isVisible(itemIndex)}]">

                                        <li v-for="(child, childIndex) in item.children" :key="childIndex">
                                            <a :title="child.title" :href="child.url"><span>{{ child.title }}</span></a>
                                        </li>
                                        
                                    </ul>
                                </li>
                                
                                <li class="col-xs-12 col-sm-12 col-md-3 social-menu" v-if="socialNavigation[0] != 0">
                                    <div class="menu-group-name">{{socialNavigation[0].title}}</div>
                                    <div class="social-links">
                                        
                                        <a v-for="(social, socialIndex) in socialNavigation[0].children" :key="socialIndex" :href="social.url" :data-phf-ico-before="social.icon" :title="social.title" target="_blank" class="ico-before" rel="nofollow"></a>
                                        
                                    </div>
                                </li>
                                
                            </ul>
                        </div>
                    </div>
                    <div class="bottom-menu">
                        <div class="module-container row">
                             <ul class="footer-links footer-options col-xs-12 col-md-6 " v-if="legalNavigation != 0">

                                <li
                                    v-for="(legalItem, legalItemIndex) in legalNavigation"
                                    :key="legalItemIndex">

                                    <a
                                        :title="legalItem.title"
                                        :href="legalItem.url">
                                        <span>
                                            {{ legalItem.title }}
                                        </span>
                                    </a>
                                </li>
                                
                            </ul>
                            <ul class="footer-links footer-legal col-xs-12 col-md-6 ">
                                
                                <li class="footer-legal_item"><span class="copyright" title="© Renault 2021">{{footer_trademark}}</span></li>
                            </ul>
                        </div>
                    </div>
                    
                </footer>
            </div>
        </div>
    </div>



</template>

<script>
    import axios from "axios";

    export default {
        name: "Footer",

        created() {
            if ("HEADER_FOOTER_SETTINGS" in window) {
                this.fetchNavigation(window.HEADER_FOOTER_SETTINGS.apiUri);
            } else {
                if (this.url) {
                    this.fetchNavigation(this.url);
                }
            }
        },

        data() {
            return {
                visibleIndex: null,
                mainFooter: [],
                basicInformation: [],
                socialNavigation: [],
                legalNavigation: []
            }
        },
        
        computed: {
            footer_trademark() {
                return this.basicInformation && this.basicInformation.meta && this.basicInformation.meta.footer_trademark;
            },
            passion() {
                return this.basicInformation && this.basicInformation.meta && this.basicInformation.meta.passion;
            }
        },
        methods: {
            fetchNavigation(apiUri) {
                axios.get(apiUri)
                    .then((response) => {
                        this.basicInformation = response.data;
                        this.mainFooter = response.data.mainfooter.schema;
                        this.socialNavigation = response.data.social_navigation.schema;
                        this.legalNavigation = response.data.legal_navigation.schema;
                    })
            },
            isVisible(itemIndex) {
                return this.visibleIndex === itemIndex;
            },

            toggle(itemIndex) {
                if (this.visibleIndex === itemIndex) {
                    this.visibleIndex = null;
                } else {
                    this.visibleIndex = Number(itemIndex);
                }
            },

            scrollToTop() {
                window.scrollTo({ top: 0, behavior: 'smooth' });
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
    * {
        font-family: NouvelR-Regular,sans-serif,Arial;
    }
    .displayBlock {
        display: block !important;
    }
    .plugin-helios-header-footer .helios-special-elements#helios-footer .page-footer footer .footer-menu li.social-menu {
        float: right;
    }
</style>
