<template>
    <div>
        <div v-if="contentIndex === null" class="mobile-dropdown">
            <ul class="mobile-dropdown-list">
                <li v-for="(navigationLink, navigationLinkIndex) in navigation" :key="navigationLinkIndex" @click="toggleDropdown(navigationLinkIndex)">
                    <a :href="navigationLink.url">
                        <span>{{ navigationLink.title }}</span>
                        <span>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 185.343 185.343" width="13" height="13" fill="#fff" class="eyqfg0d0 header-rsvka e3bhxjg0"><path d="M51.707 185.343a10.692 10.692 0 0 1-7.593-3.149 10.724 10.724 0 0 1 0-15.175l74.352-74.347L44.114 18.32c-4.194-4.194-4.194-10.987 0-15.175 4.194-4.194 10.987-4.194 15.18 0l81.934 81.934c4.194 4.194 4.194 10.987 0 15.175l-81.934 81.939a10.678 10.678 0 0 1-7.587 3.15z"></path></svg>
                        </span>
                    </a>
                </li>
            </ul>
        </div>
        <div v-if="contentIndex !== null">
            <div class="mobile-dropdown-list-expanded">
                <a href="#" @click="contentIndex = null, contentSubIndex = null">
                    <span><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 185.343 185.343" width="13" height="13" fill="#fff" class="eyqfg0d0 header-1fir606 e3bhxjg0"><path d="M51.707 185.343a10.692 10.692 0 0 1-7.593-3.149 10.724 10.724 0 0 1 0-15.175l74.352-74.347L44.114 18.32c-4.194-4.194-4.194-10.987 0-15.175 4.194-4.194 10.987-4.194 15.18 0l81.934 81.934c4.194 4.194 4.194 10.987 0 15.175l-81.934 81.939a10.678 10.678 0 0 1-7.587 3.15z"></path></svg></span>
                    <span>{{ navigation[contentIndex].title }}</span>
                </a>
            </div>
            <div :class="['expanded-list', { 'vehicle' : contentIndex === 0 }]">
                <ul>
                    <template v-if="contentIndex === 0">
                        <li v-for="(navigationItemVehicle, navigationItemVehicleIndex) in navigation[contentIndex].children" :key="navigationItemVehicleIndex">
                            <div class="subnavigation-item-container mobile-vehicle" @click="toggleSubDropdown(navigationItemVehicle, navigationItemVehicleIndex)">
                                <span :class="['mobile-vehicle-title', { 'active': contentSubIndex === navigationItemVehicleIndex }]">
                                    {{ navigationItemVehicle.title }}
                                </span>
                                <span>
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 185.343 185.343" width="13" height="13" fill="#000" :class="{ 'rotate-180': contentSubIndex === navigationItemVehicleIndex }" class="e1ciq8xl0 header-j58oa1 e3bhxjg0">
                                        <path d="M51.707 185.343a10.692 10.692 0 0 1-7.593-3.149 10.724 10.724 0 0 1 0-15.175l74.352-74.347L44.114 18.32c-4.194-4.194-4.194-10.987 0-15.175 4.194-4.194 10.987-4.194 15.18 0l81.934 81.934c4.194 4.194 4.194 10.987 0 15.175l-81.934 81.939a10.678 10.678 0 0 1-7.587 3.15z"></path>
                                    </svg>
                                </span>
                            </div>
                        <div class="mobile-subdropdown mobile-vehicle" v-if="contentSubIndex !== null && contentSubIndex === navigationItemVehicleIndex">
                                <ul>
                                    <li v-for="(subNavigationItem, subNavigationItemIndex) in navigationItemVehicle.children" :key="subNavigationItemIndex">
                                        <a :href="subNavigationItem.url">
                                            <img :src="subNavigationItem.icon" :alt="subNavigationItem.title">
                                            {{ subNavigationItem.title }}
                                        </a>
                                    </li>
                                </ul>
                                <div class="vehicle-list active">
                                    <div class="sub-nav_image_container_vehicle last-link">
                                        <a :href="navigation[contentIndex].children[contentSubIndex].url">
                                            <div class="yellow-cube-container">
                                                <span class="yellow-cube"></span>
                                                <span class="yellow-cube-plus">+</span>
                                            </div>
                                            <span>{{ navigation[contentIndex].children[contentSubIndex].title }}</span>
                                        </a>
                                    </div>
                                </div>
                            </div>
                        </li>
                    </template>

                    <template v-if="contentIndex !== 0">
                        <li v-for="(navigationItem, navigationItemIndex) in navigation[contentIndex].children" :key="navigationItemIndex">
                            <div class="subnavigation-item-container" v-if="!navigationItem.meta.image">
                                <a :href="navigationItem.url">
                                    {{ navigationItem.title }}
                                </a>
                                <span @click="toggleSubDropdown(navigationItem, navigationItemIndex)" v-if="navigationItem.children.length > 0">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 185.343 185.343" width="13" height="13" fill="#000" :class="{ 'rotate-90': contentSubIndex === navigationItemIndex }" class="e1ciq8xl0 header-j58oa1 e3bhxjg0">
                                        <path d="M51.707 185.343a10.692 10.692 0 0 1-7.593-3.149 10.724 10.724 0 0 1 0-15.175l74.352-74.347L44.114 18.32c-4.194-4.194-4.194-10.987 0-15.175 4.194-4.194 10.987-4.194 15.18 0l81.934 81.934c4.194 4.194 4.194 10.987 0 15.175l-81.934 81.939a10.678 10.678 0 0 1-7.587 3.15z"></path>
                                    </svg>
                                </span>
                            </div>
                            <div v-if="navigationItem.meta.image">
                                <a :href="navigationItem.url" style="padding-bottom: 8px;">
                                    {{ navigationItem.title }}
                                </a>
                                <div class="subnavigation-item-image-container" v-if="navigationItem.meta.image">
                                    <img :src="navigationItem.meta.image" alt="" width="auto" height="120px">
                                </div>
                            </div>
                        <div class="mobile-subdropdown" v-if="contentSubIndex !== null && contentSubIndex === navigationItemIndex">
                                <ul>
                                    <li v-for="(subNavigationItem, subNavigationItemIndex) in navigationItem.children" :key="subNavigationItemIndex">
                                        <a :href="subNavigationItem.url">
                                            {{ subNavigationItem.title }}
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </li>
                    </template>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MobileDropdown",
    props: {
        navigation: Array,
    },

    data() {
        return {
            contentIndex: null,
            contentSubIndex: null,
        }
    },

    computed: {
    },

    methods: {
        toggleDropdown(index) {
            this.contentIndex = this.contentIndex === index ? null : index;
        },

        toggleSubDropdown(navigationItem, index) {
            this.contentSubIndex = this.contentSubIndex === index ? null : index;
        }
    }
}
</script>

<style>
.rotate-90 {
  transform: rotate(90deg);
}
</style>