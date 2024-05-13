<template>
    <li :class="{'expand-box' : !item.url}">
        <a @click="toggleDropdown" :href="item.url ? item.url : '#'" :class="['dropdown', 'ico--text', isActive ? 'active' : '']" :data-phf-ico-after="item.url ? '' : item.icon" data-phf-ico-active-after="" title="Nova vozila" target="_self">
            <span>{{item.title}}</span>
        </a>
    </li>
</template>

<script>

    export default {
        name: "DropdownLink",

        props: {
            item: Object,
            itemIndex: Number,
            isActive: Boolean
        },

        data(){
            return {
            }
        },
        methods: {
            toggleDropdown() {
                this.$emit("toggleDropdown", this.itemIndex)
            }
        }

    }
</script>

<style>

</style>