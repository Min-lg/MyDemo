<!-- 响应式设计测试 -->
<template>
    <div class="page-auto-size">
        2131231231
        <div class="left"></div>
        <div class="left-bottom"></div>
    </div>
</template>

<script setup lang='ts'>
//默认1920下根HTML的size为100px
let timer:any = 0;
const BaseWidth = 1440;
const BaseFontSize = 20;
window.onresize = windowResize;
function windowResize() {
    clearTimeout(timer);
    timer = setTimeout(() => {
        let width = document.body.clientWidth;
        let widthNum = (width / BaseWidth) * BaseFontSize;
        document.documentElement.style.fontSize = widthNum + "px";
    }, 100);
}
windowResize();
</script>

<style scoped lang='scss'>
.page-auto-size {
    position: relative;
    width: 30rem;
    height: 30rem;
    background-color: red;
    .left {
        width: 10rem;
        height: 10rem;
        position: absolute;
        left: 5rem;
        top: 3rem;
        background-color: aqua;
    }
    .left-bottom {
        width: 10rem;
        height: 10rem;
        position: absolute;
        right: 5rem;
        bottom: 3rem;
        background-color: rgb(217, 0, 255);
    }
}
</style>