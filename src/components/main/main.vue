<template>
    <div class="main">
        <header class="appbar">
            <div class="header">
                <div class="container">
                    <el-row type="flex" justify="space-between" align="middle">
                        <el-col :span="8">
                            <p class="logo-title">追书神器</p>
                        </el-col>
    
                        <el-col :span="12" class="menu-btns">
                            <el-button type="primary" icon="menu"></el-button>
                            <el-button type="primary" icon="search"></el-button>
                            <el-button type="primary" icon="more"></el-button>
                        </el-col>
                    </el-row>
                </div>
            </div>
            <div class="tabs-wrap">
                <el-tabs v-model="activeName" @tab-click="handleClick" class="tabs">
                    <el-tab-pane v-for="(tab,index) in tabs" :label="tab.name" :name="tab.name" :key="tab.index"></el-tab-pane>
    
                </el-tabs>
            </div>
        </header>
        <div class="tab-show">
            <transition mode="out-in" enter-active-class="animated fadeInRight" leave-active-class="animated fadeOutRight" class="fade-animate">
                <router-view></router-view>
            </transition>
    
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                tabs: [{
                    name: '追书',
                    path: '/books'
                }, {
                    name: '社区',
                    path: '/communities'
                }, {
                    name: '发现',
                    path: '/find'
                }]
            }
        },
        computed: {
            activeName() {
                let index = this.$store.state.tabIndex;
                return this.tabs[index].name;
            }
        },
        methods: {
            handleClick(tab, event) { //切换tab
                let path = this.tabs[tab.index].path;
                let index = tab.index;
                this.$store.commit('changeTab', index)
                this.$router.push(path);
            }
        }
    }
</script>

<style lang="less">
    @mainColor: #20a0ff;
    .appbar {}
    
    .fix-margin {
        padding: 1px !important;
    }
    
    .animated {
        transition: .5s !important;
    }
    
    .header {
        width: 100%;
        background: @mainColor;
        .container {
            width: 90%;
            margin: 0 auto;
        }
        .logo-title {
            color: #fff;
        }
        .menu-btns {
            display: flex;
            justify-content: flex-end;
            button {
                margin: 0 !important;
            }
        }
    }
    
    .tabs-wrap {
        width: 100%;
        .el-tabs__nav {
            width: 100%;
            float: none !important;
            display: flex;
            justify-content: center;
            .el-tabs__active-bar {
                display: none;
            }
        }
    }
    
    .tab-show {}
</style>