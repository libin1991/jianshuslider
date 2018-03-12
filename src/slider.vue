<template>
    <div id="slider-wrapper" @mouseover="stop" @mouseout="start">
        <!-- 轮播图1，mainSlide -->
        <div class="main-slide" :style="`background: url(${slideConfig[nowIndex].src})`"></div>
        <!-- 轮播图2，extraSlide -->
        <div class="extra-slide">
            <div class="extra-slide-item" :class="slideClass(i)" v-for="(v, i) in slideConfig" :key="i" :style="`background: url(${v.src}); background-size: cover`"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'slider',
    data: function() {	
        return {
            slideInterval: null,
            nowIndex: 0,
            slideLength: this.slideConfig.length
        }
    },
    props: {
        slideConfig: {
            type: Array
        }
    },
    methods: {
        // 限制index不能超出图片列表长度
        resetIndex(i) {
            return i > this.slideLength - 1 ? i - this.slideLength : i
        },
        slideClass(i) {
            let nowIndex = this.nowIndex
            // Map就是key也可以是非字符串的Object，不用Map多写几个 if else 也可以
            let map = new Map([
                [this.resetIndex(nowIndex), 'extra-slide-top'],
                [this.resetIndex(nowIndex + 1), 'extra-slide-middle-first'],
                [this.resetIndex(nowIndex + 2), 'extra-slide-middle-second'],
                [this.resetIndex(nowIndex + 3), 'extra-slide-bottom']
            ])
            // 图片的class根据nowIndex的变化而变化
            return map.get(i) ? map.get(i) : 'extra-slide-hide'
        },
        start() {
            this.slideInterval = setInterval(() => {
                this.nowIndex = this.nowIndex > this.slideLength - 2 ? 0 : this.nowIndex + 1
                console.log(this.nowIndex)
            }, 2000)
        },
        stop() {
            clearInterval(this.slideInterval)
            this.slideInterval = null
        }
    },
    mounted() {
        this.start()
    },
    destroyed() {
        this.stop()
    }
}
</script>

<style lang="scss">
    $width: 800px;      // 容器宽度
    $height: 300px;     // 容器高度
    $bWidth: 500px;     // 大图片宽度
    $sWidth: $width - $bWidth;  // 小图片宽度
    $sHeight: $height / 2;  // 小图片高度
    #slider-wrapper{
        width: $width;
        height: $height;
        margin: 0 auto;
        cursor: pointer;
        background: #ddd;
        border-radius: 5px;
        box-shadow: 0 1px 6px rgba(0,0,0,0.117647), 0 1px 4px rgba(0,0,0,0.117647);
        display: flex;
        overflow: hidden;
        div{
            display: inline-block;
        }
    }
    .main-slide{
        width: $bWidth;
        height: $height;
        float: left;
        transition: all .4s ease;
    }
    .extra-slide{
        width: $sWidth;
        position: relative;
        .extra-slide-item{
            position: absolute;
            width: $sWidth;
            height: $sHeight;
            left: 0;
            transition: .4s ease-out;
        }
        .extra-slide-top{
            top: -$sHeight;
        }
        .extra-slide-middle-first{
            top: 0;
            z-index: 2
        }
        .extra-slide-middle-second{
            top: $sHeight;
            z-index: 2
        }
        .extra-slide-bottom{
            top: $height
        }
        .extra-slide-hide{
            display: none!important;
        }
    }
    
</style>