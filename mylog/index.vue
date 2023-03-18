<!-- 我的记录页 -->
<template>
    <div class="page_buddhachanting">
        <!-- 佛像位置 -->
        <div class="buddha_statue buddha-light"></div>
        <!-- 左边佛珠 -->
        <div class="circle_container_left" @click="handleCircleAdd(0)" v-if="[0, 2].includes(buddhaType)">
            <div class="circle_item_wrapper" :style="`transform: rotate(${clickLeftIndex * 36}deg)`">
                <div class="item" v-for="itemIndex in 10" :class="{ bigItem: getBigItemLeftIndex == itemIndex - 1 }"></div>
            </div>
        </div>
        <!-- 右边佛珠 -->
        <div class="circle_container_right" @click="handleCircleAdd(1)" v-if="[1, 2].includes(buddhaType)">
            <div class="circle_item_wrapper" :style="`transform: rotate(${clickRightIndex * -36}deg)`">
                <div class="item" v-for="itemIndex in 10" :class="{ bigItem: getBigItemRightIndex == itemIndex - 1 }"></div>
            </div>
        </div>
        <!-- 左边文字 -->
        <div class="catching-fish-movies">
            <transition-group appear name="left_moves" tag="div" v-on:after-enter="handleLeftLeave">
                <template v-for="item in leftTextList">
                    <div v-if="item.key" class="left_text_move" v-bind:key="item.key" :id="item.key">
                        <span class="gift-num" v-html="item.desc"></span>
                    </div>
                </template>
            </transition-group>
        </div>
        <!-- 右边文字 -->
        <div class="catching-fish-movies">
            <transition-group appear name="catchFishMovie" tag="div" v-on:after-enter="handlerightLeave">
                <template v-for="item in rightTextList">
                    <div v-if="item.key" class="right_text_move" v-bind:key="item.key" :id="item.key">
                        <span class="gift-num" v-html="item.desc"></span>
                    </div>
                </template>
            </transition-group>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            bigCircle_right: 7, // 放大的珠子index
            bigCircle_left: 8, // 放大的珠子index
            clickLeftIndex: 1, // 点击了多少次
            clickRightIndex: 1, // 点击了多少次
            leftTextList: [], // 动画文案
            rightTextList: [], // 动画文案
            buddhaType: 2, // 0 左边 1右边 2 两边都显示
        };
    },
    computed: {
        getBigItemLeftIndex() {
            return this.bigCircle_left;
        },
        getBigItemRightIndex() {
            return this.bigCircle_right;
        },
    },
    created() {},
    methods: {
        // type: 0||1 0点击左边 1 点击右边
        handleCircleAdd(type) {
            const key = new Date().getTime() + parseInt(Math.random() * 10000000);
            if (type == 0) {
                // 左边佛珠转动
                this.bigCircle_left = this.bigCircle_left <= 0 ? 9 : this.bigCircle_left - 1;
                this.clickLeftIndex = this.clickLeftIndex + 1;
                this.leftTextList.push({
                    desc: "阿弥陀佛lllllllllll",
                    key,
                });
            } else {
                // 右边佛珠转动
                this.bigCircle_right = this.bigCircle_right >= 9 ? 0 : this.bigCircle_right + 1;
                this.clickRightIndex = this.clickRightIndex + 1;
                this.rightTextList.push({
                    desc: "阿弥陀佛2",
                    key,
                });
            }
        },
        handleLeftLeave(el) {
            let key = el.getAttribute("id");
            let i = 0;
            while (i < this.leftTextList.length) {
                if (this.leftTextList[i].key == key) {
                    this.leftTextList.splice(i, 1);
                    continue;
                }
                i++;
            }
        },
        handlerightLeave(el) {
            let key = el.getAttribute("id");
            let i = 0;
            while (i < this.rightTextList.length) {
                if (this.rightTextList[i].key == key) {
                    this.rightTextList.splice(i, 1);
                    continue;
                }
                i++;
            }
        },
    },
};
</script>
<style lang="scss" scoped>
@import "~@styles/funs";
@import "./style.scss";
</style>
