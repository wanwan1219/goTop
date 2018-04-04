<template>
    <div class="suspend">
        <div class="cu" :class='{"qr":qrOld,"qrhover":qrIsShow}' @mouseover="showqr" @mouseout="hideqr" >
            <img src="../../static/images/active_sign/qr_code.svg" alt="">
            <p>关注我们</p>
            <div v-show="qrIsShow" class="bigqr">
                <img src="./../../assets/img/Bitmap.png" alt="">
                <p>扫码关注</p>
            </div>
        </div>
        <div class="online cu" onclick="qimoChatClick()">
            <div class="dotted"></div>
            <img src="../../static/images/active_sign/online_consulting.svg" alt="">
            <p>在线咨询</p>
            <div class="dotted"></div>
        </div>
        <div class="cu" :class='{"qr":qrOld,"apphover":qrAppshow}' @mouseover="showApp" @mouseout="hideApp" >
            <img class="app_img"  src="../../static/images/active_sign/load.svg" alt="">
            <p class="app_p">App下载</p>
            <div v-show="qrAppshow" class="bigApp">
                <img src="../../static/images/active_sign/app_load.png" alt="">
                <p >扫码下载</p>
            </div> 
        </div>
        <div class="to-top cu" @click="toTop(0.1,'')">
            <div class="dotted"></div>
            <img src="../../static/images/active_sign/to_top.svg" alt="">
            <p>返回顶部</p>
        </div>
    </div>
</template>

<script>
export default {
    data(){
       return{
            qrIsShow:false,
            qrOld:true,
            qrAppshow:false,
       }
    },
    methods:{
        showqr(){
            this.qrIsShow=true;
        },
        hideqr(){
            this.qrIsShow=false;
        },
        showApp(){
            this.qrAppshow=true;
        },
        hideApp(){
            this.qrAppshow=false;
        },
        toTop(acceleration,time) {
            acceleration = acceleration || 0.1;
            time = time || 16;

            var x1 = 0;
            var y1 = 0;
            var x2 = 0;
            var y2 = 0;
            var x3 = 0;
            var y3 = 0;

            if (document.documentElement) {
                x1 = document.documentElement.scrollLeft || 0;
                y1 = document.documentElement.scrollTop || 0;
            }
            if (document.body) {
                x2 = document.body.scrollLeft || 0;
                y2 = document.body.scrollTop || 0;
            }
            var x3 = window.scrollX || 0;
            var y3 = window.scrollY || 0;

            // 滚动条到页面顶部的水平距离
            var x = Math.max(x1, Math.max(x2, x3));
            // 滚动条到页面顶部的垂直距离
            var y = Math.max(y1, Math.max(y2, y3));

            // 滚动距离 = 目前距离 / 速度, 因为距离原来越小, 速度是大于 1 的数, 所以滚动距离会越来越小
            var speed = 1 + acceleration;
            window.scrollTo(Math.floor(x / speed), Math.floor(y / speed));
            // 如果距离不为零, 继续调用迭代本函数
            if(x > 0 || y > 0) {
                window.setTimeout(this.toTop, time);
            }
        }
    },
    mounted() {
        qimo(this.userInfo.user_id||'', this.userInfo.nick_name||'');
    },
    computed: {
        userInfo() {
            return this.$store.getters.uInfo || {};
        }
    },
}
</script>

<style scoped>
    .suspend{
        width: 64px;
        height: 255px;
        background: #00A953;
        box-shadow: 0 0 2px 0 #54C7FC;
        border-radius: 8px;
        position: fixed;
        z-index: 9999;
        right: 20px;
        bottom: 90px;
        display: flex;
        flex-direction: column;
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
    }
    .suspend > div{
        flex: 1;
        box-sizing: border-box;
    }
    .dotted{
        border-bottom: 2px dotted #fff;
        margin: 0 10px;
    }
    .suspend > div img{
        width: 25px;
        height: 20px;
        display: block;
        margin:10px auto 0;
    }
    .suspend > div p{
        text-align: center;
        margin-top:5px;
        margin-bottom: 5px; 
    }
    .suspend .qr img{
        width: 25px;
        height: 25px;
        display: block;
    }
    .suspend .qr p{
        margin-bottom: 13px;
    }
    .suspend .qr .app_p{
        margin-bottom: 3px;
    }
    .suspend .qr .app_img{
        margin-top: 5px;
    }
    .bigqr{
        position: absolute;
        left: -123px;
        top: 0;
        width: 123px;
        height: 152px;
        background: #00A953;
        border-radius: 4px 0 0 4px;
    }

    .bigApp{
        position: absolute;
        left: -123px;
        top: 132px;
        width: 123px;
        height: 152px;
        background: #00A953;
        border-radius: 4px 0 0 4px;
    }
    
    .suspend .qr .bigApp img{
        width: 113px;
        height: 113px;
    }

    .suspend .qr .bigApp p{
        text-align: center;
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
    }

    .suspend .qr .bigqr img{
        width: 113px;
        height: 113px;
    }

    .suspend .qr .bigqr p{
        text-align: center;
        font-family: PingFangSC-Regular;
        font-size: 12px;
        color: #FFFFFF;
    }
    .suspend .qrhover{
        background: #00A953;
        border-radius: 0 8px 0 0;
    }
    
    .suspend .apphover{
        background: #00A953;
        border-radius: 0 0 0 0;
    }

</style>
