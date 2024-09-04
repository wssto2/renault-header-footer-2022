<template>
    <div v-if="dropdownActiveType !== null">
        <div v-if="itemIndex === 0 && !item.url && item != 0 && dropdownActiveType === 0" :class="['expand-container', {'is-active' : dropdownActive}]">
            <div class="expand grid-row">
                <div class="sub-nav sub-nav_vehicles">
                    <ul>
                    <li v-for="(dropdownLink, dropdownLinkIndex) in item.children" :key="dropdownLinkIndex">
                        <a @click="toggleCarCategory(dropdownLinkIndex)" :class="['sub-nav_link', dropdownLinkIndex === vehicleDropdownActive ? 'active' : '']" href="#" target="_self" title="Renault SELECTION">
                        <span>{{dropdownLink.title}}</span>
                        </a>
                    </li>
                    </ul>
                    <div :class="['vehicle-list', dropdownLinkItemIndex === vehicleDropdownActive ? 'active' : '']" v-for="(dropdownLinkItem, dropdownLinkItemIndex) in item.children" :key="dropdownLinkItemIndex">
                        <div class="sub-nav_image_container_vehicle" v-for="(childItem, childIndex) in dropdownLinkItem.children" :key="childIndex">
                            <a :href="childItem.url">
                                <img v-if="childItem.icon" :src="childItem.icon" :alt="childItem.title">
                                <span>{{ childItem.title }}</span>
                            </a>
                        </div>
                        <div class="sub-nav_image_container_vehicle last-link">
                            <a :href="dropdownLinkItem.url">
                                <div class="yellow-cube-container">
                                    <span class="yellow-cube"></span>
                                    <span class="yellow-cube-plus">+</span>
                                </div>
                                <span>{{ dropdownLinkItem.title }}</span>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>



                                        
        <div v-if="itemIndex !== 0 && !item.url && item != 0 && itemIndex === dropdownActiveType" :class="['expand-container', {'is-active' : dropdownActive}]">
            <div class="expand grid-row">
                <div class="sub-nav  ">
                    <ul>
                        <li v-for="(dropdownLink, dropdownLinkIndex) in item.children" :key="dropdownLinkIndex" :class="['sub-nav-item', { 'has-image': dropdownLink.meta.image }]">

                            <!-- Main List Item Content -->
                            <a class="sub-nav_link" :href="dropdownLink.url" target="_self" :title="dropdownLink.title">
                                <span>{{ dropdownLink.title }}</span>
                            </a>
                            
                            <!-- Sub-navigation children -->
                            <ul class="sub-nav_children">
                                <li
                                    class="sub-nav_children-item"
                                    v-for="(dropdownLinkChild, dropdownLinkChildIndex) in item.children[dropdownLinkIndex].children"
                                    :key="dropdownLinkChildIndex"
                                >
                                    <a class="sub-nav_link_children" :href="dropdownLinkChild.url" :target="dropdownLinkChild.target != null ? dropdownLinkChild.target : '_self'" :title="dropdownLinkChild.title">
                                        <span>{{ dropdownLinkChild.title }}</span>
                                    </a>
                                </li>
                            </ul>
                            
                            <!-- Image Container -->
                            <div class="sub-nav_image_container">
                                <img v-if="dropdownLink.meta.image" :src="dropdownLink.meta.image" :alt="dropdownLink.title">
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

</template>

<script>

    export default {
        name: "Dropdown",

        props: {
            item: Object,
            itemIndex: Number,
            dropdownActiveType: Number
        },

        data(){
            return {
                dropdownActive: false,
                vehicleDropdownActive: 0
            }
        },
        created() {
            window.addEventListener('click', this.close)
        },
        beforeDestroy(){
            window.removeEventListener('click', this.close)
        },
        methods: {
            toggleCarCategory(index){
                this.vehicleDropdownActive = index;
            },
            close(e) {
                if(! this.$el.contains(e.target)){
                    if(this.dropdownActive){
                        this.$emit("showModal", null)
                    }
                    this.dropdownActive = false;
                }
            }
        }

    }
</script>

<style>

</style>