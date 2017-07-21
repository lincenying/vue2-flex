<template>
<div class="g-mn">
    <el-row :gutter="20">
        <el-col :span="8">
            <h1>父容器</h1>
            <div>
                <el-form label-width="220px">
                    <el-form-item label="flex-direction">
                        <el-select v-model="flexDirection">
                            <el-option v-for="item in options1" :label="item.value" :value="item.value"> </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="flex-wrap">
                        <el-select v-model="flexWrap">
                            <el-option v-for="item in options2" :label="item.value" :value="item.value"> </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="justify-content">
                        <el-select v-model="justifyContent">
                            <el-option v-for="item in options3" :label="item.value" :value="item.value"> </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="align-items">
                        <el-select v-model="alignItems">
                            <el-option v-for="item in options4" :label="item.value" :value="item.value"> </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="align-content">
                        <el-select v-model="alignContent">
                            <el-option v-for="item in options5" :label="item.value" :value="item.value"> </el-option>
                        </el-select>
                    </el-form-item>
                </el-form>
            </div>
            <h1>子容器</h1>
            <div>
                <div class="block">
                    <span class="demonstration">子容器数量</span>
                    <el-slider v-model="itemNum" :min="1" :max="10"></el-slider>
                </div>
                <div class="block">
                    <span class="demonstration">子容器宽度</span>
                    <el-slider v-model="itemWidth" :min="10" :max="100" :step="1"></el-slider>
                </div>
            </div>
        </el-col>
        <el-col :span="16">
            <transition-group class="grid-content" name="list-complete" tag="div" :style="{
                display: 'flex',
                flexDirection: flexDirection,
                flexWrap: flexWrap,
                justifyContent: justifyContent,
                alignItems: alignItems,
                alignContent: alignContent
            }">
                <div v-for="(item, index) in itemLists" :key="index" :style="{
                    width: itemWidth + '%',
                    alignSelf: item.alignSelf,
                    flexBasis: item.flexBasis,
                    flexGrow: item.flexGrow,
                    flexShrink: item.flexShrink,
                    order: item.order
                }" v-text="'子容器: ' + index"></div>
            </transition-group>
        </el-col>
    </el-row>
    <el-row>
        <el-col :span="24">
            <h1>子容器配置</h1>
            <div class="item">
                <div v-for="(item, index) in itemLists">
                    <div class="block">
                        <span class="demonstration">子容器: {{ index }}</span>
                        <div></div>
                    </div>
                    <div class="block">
                        <span class="demonstration">order</span>
                        <el-slider v-model="item.order" :min="-10" :max="10"></el-slider>
                    </div>
                    <div class="block">
                        <span class="demonstration">flex-grow</span>
                        <el-slider v-model="item.flexGrow" :min="0" :max="10"></el-slider>
                    </div>
                    <div class="block">
                        <span class="demonstration">flex-shrink</span>
                        <el-slider v-model="item.flexShrink" :min="0" :max="10"></el-slider>
                    </div>
                    <div class="block">
                        <span class="demonstration">flex-basis</span>
                        <el-input placeholder="请输入内容" v-model="item.flexBasis"> </el-input>
                    </div>
                    <div class="block">
                        <span class="demonstration">align-self</span>
                        <el-select v-model="item.alignSelf">
                            <el-option :label="'auto'" :value="'auto'"> </el-option>
                            <el-option :label="'flex-start'" :value="'flex-start'"> </el-option>
                            <el-option :label="'flex-end'" :value="'flex-end'"> </el-option>
                            <el-option :label="'center'" :value="'center'"> </el-option>
                            <el-option :label="'baseline'" :value="'baseline'"> </el-option>
                            <el-option :label="'stretch'" :value="'stretch'"> </el-option>
                        </el-select>
                    </div>
                </div>
            </div>
        </el-col>
    </el-row>
    <el-row>
        <el-col :span="24">
            <h1>父容器CSS:</h1>
            <pre>
.items {
    display: flex;
    flex-direction: {{ flexDirection }};
    flex-wrap: {{ flexWrap }};
    justify-content: {{ justifyContent }};
    align-items: {{ alignItems }};
    align-content: {{ alignContent }};
}
            </pre>
        </el-col>
    </el-row>
    <el-row>
        <el-col :span="24">
            <h1>子容器CSS:</h1>
            <pre v-for="(item, index) in itemLists">
.item-{{ index }} {
    align-self: {{ item.alignSelf }};
    flex: {{ item.flexGrow }} {{ item.flexShrink }} {{ item.flexBasis }};
    order: {{ item.order }};
}
            </pre>
        </el-col>
    </el-row>
</div>
</template>

<script lang="babel">
import elRow from 'element-ui/lib/row'
import elCol from 'element-ui/lib/col'
import 'element-ui/lib/theme-default/row.css'
import 'element-ui/lib/theme-default/col.css'

import elSelect from 'element-ui/lib/select'
import elOption from 'element-ui/lib/option'
import 'element-ui/lib/theme-default/select.css'
import 'element-ui/lib/theme-default/option.css'

import elForm from 'element-ui/lib/form'
import 'element-ui/lib/theme-default/form.css'
import elFormItem from 'element-ui/lib/form-item'
import 'element-ui/lib/theme-default/form-item.css'

import elSlider from 'element-ui/lib/slider'
import 'element-ui/lib/theme-default/slider.css'

import elInput from 'element-ui/lib/input'
import 'element-ui/lib/theme-default/input.css'

export default {
    components: {
        elRow,
        elCol,
        elSelect,
        elOption,
        elFormItem,
        elForm,
        elSlider,
        elInput
    },
    data() {
        return {
            flexDirection: 'row',
            flexWrap: 'nowrap',
            justifyContent: 'flex-start',
            alignItems: 'stretch',
            alignContent: 'stretch',
            options1: [{
                value: 'row'
            }, {
                value: 'row-reverse'
            }, {
                value: 'column'
            }, {
                value: 'column-reverse'
            }],
            options2: [{
                value: 'nowrap'
            }, {
                value: 'wrap'
            }, {
                value: 'wrap-reverse'
            }],
            options3: [{
                value: 'flex-start'
            }, {
                value: 'flex-end'
            }, {
                value: 'center'
            }, {
                value: 'space-between'
            }, {
                value: 'space-around'
            }],
            options4: [{
                value: 'stretch'
            }, {
                value: 'flex-start'
            }, {
                value: 'flex-end'
            }, {
                value: 'center'
            }, {
                value: 'baseline'
            }],
            options5: [{
                value: 'stretch'
            }, {
                value: 'flex-start'
            }, {
                value: 'flex-end'
            }, {
                value: 'center'
            }, {
                value: 'space-between'
            }, {
                value: 'space-around'
            }],
            itemNum: 3,
            itemWidth: 30,
            itemLists: [{
                order: 0,
                flexGrow: 0,
                flexShrink: 1,
                flexBasis: 'auto',
                alignSelf: 'auto'
            }, {
                order: 0,
                flexGrow: 0,
                flexShrink: 1,
                flexBasis: 'auto',
                alignSelf: 'auto'
            }, {
                order: 0,
                flexGrow: 0,
                flexShrink: 1,
                flexBasis: 'auto',
                alignSelf: 'auto'
            }]
        }
    },
    computed: {

    },
    methods: {

    },
    mounted() {},
    watch: {
        itemNum(val, oldVal) {
            if (val > oldVal) {
                const addNum = val - oldVal
                for (let i = 0; i < addNum; i++) {
                    this.itemLists.push({
                        order: 0,
                        flexGrow: 0,
                        flexShrink: 1,
                        flexBasis: 'auto',
                        alignSelf: 'auto'
                    })
                }
            } else {
                const subNum = oldVal - val
                this.itemLists.splice(val, subNum)
            }
        }
    }
}
</script>
<style lang="less">
.g-mn {
    .block {
        display: flex;
        align-items: center;
        .demonstration {
            width: 220px;
        }
        .el-slider {
            flex: auto;
        }
    }
    .item {
        .block {
            margin-bottom: 10px;
            .demonstration {
                width: 100px;
            }
        }
    }
}
.grid-content {
    background: #ccc;
    border: 1px solid #f00;
    border-radius: 10px;
    height: 500px;
    padding: 10px;
    & > div {
        height: 100px;
        border: 1px solid blue;
        border-radius: 10px;
        background: #fff;
        text-align: center;
    }
}
.item {
    display: flex;
    flex-wrap: wrap;
    & > div {
        border: 1px solid blue;
        border-radius: 10px;
        margin-right: 10px;
        margin-bottom: 10px;
        padding: 10px;
        width: 18%;
        flex: none;
    }
}
.list-complete-item {
    transition: all 1s;
    margin-right: 10px;
}
.list-complete-enter,
.list-complete-leave-active {
    opacity: 0;
    transform: translateY(30px);
}
.list-complete-leave-active {
    position: absolute;
}
</style>
