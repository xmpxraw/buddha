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
import { ref } from "vue";

export default {
    setup() {
        const bigCircleRight = ref(7); // 放大的珠子index
        const bigCircleLeft = ref(8); // 放大的珠子index
        const clickLeftIndex = ref(1); // 点击了多少次
        const clickRightIndex = ref(1); // 点击了多少次
        const leftTextList = ref([]); // 动画文案
        const rightTextList = ref([]); // 动画文案
        const buddhaType = ref(2); // 0 左边 1右边 2 两边都显示

        function handleCircleAdd(type) {
            const key = Date.now() + parseInt(Math.random() * 10000000);
            if (type === 0) {
                // 左边佛珠转动
                bigCircleLeft.value = bigCircleLeft.value <= 0 ? 9 : bigCircleLeft.value - 1;
                clickLeftIndex.value += 1;
                leftTextList.value.push({
                    desc: "阿弥陀佛lllllllllll",
                    key,
                });
            } else {
                // 右边佛珠转动
                bigCircleRight.value = bigCircleRight.value >= 9 ? 0 : bigCircleRight.value + 1;
                clickRightIndex.value += 1;
                rightTextList.value.push({
                    desc: "阿弥陀佛2",
                    key,
                });
            }
        }

        function handleLeftLeave(el) {
            const key = el.getAttribute("id");
            let i = 0;
            while (i < leftTextList.value.length) {
                if (leftTextList.value[i].key === key) {
                    leftTextList.value.splice(i, 1);
                    continue;
                }
                i++;
            }
        }

        function handlerightLeave(el) {
            const key = el.getAttribute("id");
            let i = 0;
            while (i < rightTextList.value.length) {
                if (rightTextList.value[i].key === key) {
                    rightTextList.value.splice(i, 1);
                    continue;
                }
                i++;
            }
        }

        return {
            bigCircle_right: bigCircleRight,
            bigCircle_left: bigCircleLeft,
            clickLeftIndex,
            clickRightIndex,
            leftTextList,
            rightTextList,
            buddhaType,
            handleCircleAdd,
            handleLeftLeave,
            handlerightLeave,
        };
    },
};
</script>
<style lang="scss" scoped>
@import "~@styles/funs";
@import "./style.scss";
</style>
