<template>
    <div class="sidebar">
        <div class="sidebar-backdrop" @click="closeSidebarPanel" v-if="isPanelOpen"></div>
        <transition name="slide">
            <div v-if="isPanelOpen" class="sidebar-panel">
                <ul role="navigation" class="sidebar-panel-nav">
                    <li><div class="sidebar-panel-item"><Search /></div></li>
                    <li><router-link class="sidebar-panel-item" v-bind:to="'/podcasts'">PODCASTS</router-link></li>
                    <li><router-link class="sidebar-panel-item" v-bind:to="'/shows'">SHOWS</router-link></li>
                    <li><router-link class="sidebar-panel-item" v-bind:to="'/prog'">PROG</router-link></li>
                    <li><router-link class="sidebar-panel-item" v-bind:to="'/actions'">REPORTAGES/ACTIONS</router-link></li>
                    <li><router-link class="sidebar-panel-item" v-bind:to="'/raptz'">RAPTZ</router-link></li>
                </ul>
            </div>
        </transition>
    </div>
</template>
<script>
import Search from '@/components/header/Search';

export default {
    name:"Sidebar",
    components: {
        Search
    },
    methods: {
        closeSidebarPanel(){
            this.$store.commit('toggleNav');
        }
    },
    computed: {
        isPanelOpen() {
            return this.$store.state.isNavOpen
        }
    }
}
</script>
<style>
    .slide-enter-active,
    .slide-leave-active
    {
        transition: transform 0.2s ease;
    }

    .slide-enter,
    .slide-leave-to {
        transform: translateX(-100%);
        transition: all 150ms ease-in 0s
    }

    .sidebar-backdrop {
        background-color: #233045(0,0,0,.5);
        width: 100vw;
        height: 100vh;
        position: fixed;
        top: 0;
        left: 0;
        cursor: pointer;
    }

    .sidebar-panel {
        overflow-y: auto;
        background-color: #233045;
        position: fixed;
        left: 0;
        top: 0;
        height: 100vh;
        z-index: 999;
        padding: 3rem 20px 2rem 20px;
        width: 300px;
    }

    .sidebar-panel-nav {
        display:flex;
        flex-direction: column;
    }

    .sidebar-panel-item{
        display:inline-block;
        padding:1em;
    }
</style>