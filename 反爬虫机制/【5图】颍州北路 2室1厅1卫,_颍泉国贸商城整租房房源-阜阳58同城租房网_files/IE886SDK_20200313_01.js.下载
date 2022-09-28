(function (global, factory) {
    typeof exports === 'object' && typeof module !== 'undefined' ? module.exports = factory() :
    typeof define === 'function' && define.amd ? define(factory) :
    (global = global || self, global.IE886SDK = factory());
}(this, (function () { 'use strict';

    /*
        参数说明：
        var IE886config = {
            openBrowserJudge: true/false (true:需要浏览器版本控制逻辑，默认为判断IE8及以下版本)，
            autoClose: true/false (是否支持弹框自动关闭)
            autoTime: 3000 (autoClose为true时，可设置多少秒后关闭弹窗)
            clickClose: true/false (是否支持手动关闭)
            intervalDay: 15 (设置频次，每15天会弹出一次)
            totalDay: 3 (设置上限，单位为年，每年最多展示3次)
        }

        调用示例：
        var IE886config = {
            openBrowserJudge: true,
            autoClose: false,
            autoTime: 5000,
            clickClose: true,
            intervalDay: 15,
            totalDay: 3
        };

        IE886SDK(IE886config);
    */

    function IE886SDK (IE886config) {
        var params = {
            openBrowserJudge: IE886config.openBrowserJudge === false ? IE886config.openBrowserJudge : true,
            clickClose: IE886config.clickClose === false ? IE886config.clickClose : true,
            autoClose: IE886config.autoClose === true ? IE886config.autoClose : false,
            autoTime: IE886config.autoTime ? IE886config.autoTime : 5000,
            intervalDay: IE886config.intervalDay ? IE886config.intervalDay : 15,
            totalDay: IE886config.totalDay ? IE886config.totalDay : 3
        };

        Ie886Main();

        function Ie886Main(){
            params.openBrowserJudge ? judgeIe8() : showUpdateDialog(params.intervalDay, params.totalDay);
        }

        // 获取浏览器类型
        function getBrowserInfo(){
            var agent = navigator.userAgent.toLowerCase() ;
            
            var regStr_ie = /msie [\d.]+;/gi ;
            var regStr_ff = /firefox\/[\d.]+/gi;
            var regStr_chrome = /chrome\/[\d.]+/gi ;
            var regStr_saf = /safari\/[\d.]+/gi ;

            var isIE11 = (navigator.userAgent.toLowerCase().indexOf("trident") > -1 && navigator.userAgent.indexOf("rv") > -1);
            var browser = " ";
            //IE
            if(isIE11 || agent.indexOf("msie") > 0){
                browser = isIE11 ? ["msie 11.0;"] : agent.match(regStr_ie) ;
            }
            
            //firefox
            if(agent.indexOf("firefox") > 0){
                browser = agent.match(regStr_ff) ;
            }
            
            //Safari
            if(agent.indexOf("safari") > 0 && agent.indexOf("chrome") < 0){
                browser = agent.match(regStr_saf) ;
            }
            
            //Chrome
            if(agent.indexOf("chrome") > 0){
                browser = agent.match(regStr_chrome) ;
            }

            return browser + "";
            
        }

        // 获取浏览器版本
        function getBrowserVerInfo(browser) {
            return browser.replace(/[^0-9.]/ig,""); 
        }

        // 判断是否IE8以下浏览器
        function judgeIe8() {
            // 浏览器
            var browser = getBrowserInfo();
            // 浏览器版本
            var verInfo = getBrowserVerInfo(browser);

            if(browser.indexOf("msie") > -1 && verInfo < 9){
                showUpdateDialog(params.intervalDay, params.totalDay);
            }

            return
        }

        // 提醒升级弹框DOM
        function createToast() {
            var alertHtml = '';
            alertHtml += 
            '<div class="toast-mask" id="toast-mask"></div>\
        <div class="toast-wrapper" id="toast-wrapper">\
            <div class="toast-close"><img id="toast-close" src="https://pages.anjukestatic.com/usersite/site/img/common/icon_close@3x.png" alt="" class="broswer-icon"></div>\
            <div class="toast-title"><img src="https://pages.anjukestatic.com/usersite/site/img/common/icon_ts@2x.png" alt="" class="broswer-icon"><span>您当前的浏览器版本过低！</span></div>\
            <div class="toast-desc">可能存在安全风险，建议升级您的浏览器！</div>\
            <div class="toast-recommend">官方推荐浏览器：</div>\
            <div class="toast-download">（请点击以下图标进行下载升级）</div>\
            <div class="toast-browser">\
                <a href="https://pc.qq.com/detail/1/detail_2661.html" class="broswer-item" style="padding-right: 39px;"><img src="https://pages.anjukestatic.com/usersite/site/img/common/icon_google@2x.png" alt="" class="broswer-icon"><div>谷歌</div></a>\
                <a href="http://www.firefox.com.cn/" class="broswer-item" style="padding-right: 39px;"><img src="https://pages.anjukestatic.com/usersite/site/img/common/icon_firefox@2x.png" alt="" class="broswer-icon"><div>火狐</div></a>\
                <a href="http://browser.360.cn/se/" class="broswer-item" style="padding-right: 39px;"><img src="https://pages.anjukestatic.com/usersite/site/img/common/icon_360@2x.png" alt="" class="broswer-icon"><div>360</div></a>\
                <a href="https://pc.qq.com/detail/7/detail_11527.html" class="broswer-item"><img src="https://pages.anjukestatic.com/usersite/site/img/common/icon_ie@2x.png" alt="" class="broswer-icon"><div>IE9及以上</div></a>\
            </div>\
        </div>\
        ';
            var dom = document.createElement("div"); 
            dom.innerHTML = alertHtml;
            document.body.appendChild(dom);
        }

        // 弹框样式
        function toastStyle() {
            var css = '.hidden-mask{display:none}\
                    .toast-mask{position: fixed;height: 100%;width:100%;top: 0px;bottom: 0px;right: 0px;left: 0px;background: #000;opacity: 0.5;filter:Alpha(opacity=50);z-index: 50000;}\
                    .toast-wrapper{width: 440px;height: 262px;background: #fff;box-shadow: 0px 2px 8px 0px rgba(0,0,0,0.2);border-radius: 2px;position: fixed;top: 50%;left: 50%;margin-left:-220px;margin-top:-131px;z-index: 50001;text-align: center;}\
                    .toast-wrapper .toast-close{margin-top: 10px;text-align: right;margin-right: 10px;height: 16px;}\
                    .toast-wrapper .toast-close img{width:10px; height:10px;}\
                    .toast-wrapper .toast-title{width:100%;margin:auto;}\
                    .toast-wrapper .toast-title img{width: 24px;height: 24px;margin-right: 10px;vertical-align: middle;text-align: center;}\
                    .toast-wrapper .toast-title span{font-size: 20px;line-height: 20px;font-weight: 500;color: #F53732;vertical-align: middle;text-align: center;}\
                    .toast-wrapper .toast-desc{font-size: 16px;line-height:16px; font-weight: 400;color: #333;margin-top: 13px;}\
                    .toast-wrapper .toast-recommend{font-size: 14px;line-height:14px;font-weight: 500;color: #333;margin-top: 25px;}\
                    .toast-wrapper .toast-download{font-size: 12px;font-weight: 400;color:#999;margin-top: 10px;}\
                    .toast-wrapper .toast-browser{margin: 20px auto 0px auto; width:100%;}\
                    .toast-wrapper .toast-browser .broswer-item{display: inline-block; color:#333;}\
                    .toast-wrapper .toast-browser .broswer-item div{font-size:14px;}\
                    .toast-wrapper .toast-browser .broswer-item img{width: 50px;height: 50px;}';

            var style = document.createElement('style');
            style.type = 'text/css';
            
            style.styleSheet ? style.styleSheet.cssText = css : style.innerHTML = css;
            
            document.getElementsByTagName('head')[0].appendChild(style);
        }  

        // 事件监听
        function bindEvent() {
            if (params.clickClose === true && params.autoClose === false) {
                clickEvent();
            }else if (params.clickClose === true && params.autoClose === true) {
                clickEvent();
                autoEvent();
            }else if(params.clickClose === false && params.autoClose === true){
                addClass(document.getElementById('toast-close'), 'hidden-mask');
                autoEvent();
            }else if(params.clickClose === false && params.autoClose === false){
                addClass(document.getElementById('toast-close'), 'hidden-mask');
            }else {
                clickEvent();
            }

            function clickEvent() {
                // 点击蒙层关闭弹层
                document.getElementById("toast-mask").onclick=function(){
                    addClass(document.getElementById('toast-mask'), 'hidden-mask');
                    addClass(document.getElementById('toast-wrapper'), 'hidden-mask');
                };
                // 点击关闭按钮关闭弹层
                document.getElementById("toast-close").onclick=function(){
                    addClass(document.getElementById('toast-mask'), 'hidden-mask');
                    addClass(document.getElementById('toast-wrapper'), 'hidden-mask');
                };
            }

            function autoEvent() {
                setTimeout(function(){
                    addClass(document.getElementById('toast-mask'), 'hidden-mask');
                    addClass(document.getElementById('toast-wrapper'), 'hidden-mask');
                }, params.autoTime);
            }
        }

        // 给元素添加类名(兼容IE低版本)
        function addClass(el, className){
            if(hasClass(el, className)){
                return
            }
            var newClass = el.className.split(' ');
            newClass.push(className);
            el.className = newClass.join(' ');
        }
        function hasClass(el, className){
            var reg = new RegExp('(^|\\s)' + className + '(\\s|$)');
            return reg.test(el.className)
        }

        // 初始化弹框
        function initUpdateDialog(){
            toastStyle();
            createToast();
            bindEvent();
        }

        // 操作cookie(标记用户登录时间)
        function handleCookie(method, key, val, time) {
            switch (method) {
                case 'get' : {
                /*获取cookie参数*/
                    var getCookie = document.cookie.replace(/[ ]/g,"");
                    var arrCookie = getCookie.split(";");
                    var tips;
                    for(var i=0;i<arrCookie.length;i++){
                        var arr=arrCookie[i].split("=");
                        if(key==arr[0]){
                            tips=arr[1];
                            break;
                        }
                    }
                    return tips;
                }
                case 'set' : {
                    var date=new Date(); //获取当前时间
                    var expiresDays=time;  //将date设置为n天以后的时间
                    date.setTime(date.getTime()+expiresDays*24*3600*1000); //格式化为cookie识别的时间
                    document.cookie=key + "=" + val + ";path=/;";  //设置cookie
                    break
                }
                case 'remove': {
                    var date = new Date();
                    date.setTime(date.getTime()-10000);
                    document.cookie = key + "=v; expires =" +date.toGMTString();
                    break
                }
                default : {
                    return false
                }
            }
        }

        //判断距离上次访问间隔天数
        function selectDay(begintime, endtime){   
            var nTime = endtime - begintime;  
            var day =Math.floor(nTime/86400000);
            return day;
        }

        // 展示弹框（频次逻辑）
        function showUpdateDialog(space, max){
            // 上次浏览页面时间戳
            var LastBrowse = handleCookie("get","pcLastLogin");

            // 当前时间戳
            var timestamp = new Date().getTime();
            handleCookie("set",'pcLastLogin', timestamp);
            
            // 距离上次相差时间
            var spaceTime = selectDay(LastBrowse, timestamp);

            //每年第一次浏览时间戳 
            if(!handleCookie("get","loginTime")){
                handleCookie("set",'pcFirstLogin', timestamp);
            }
            var FirstBrowse = handleCookie("get","pcFirstLogin");
            // 每满一年清空一次计数器
            if(selectDay(FirstBrowse, timestamp) > 365){handleCookie("remove","loginTime");}

            // 弹框展示计数器
            if (!handleCookie("get","loginTime") || (handleCookie("get","loginTime") && handleCookie("get","loginTime") < max && spaceTime > space)) {
                var totalLoginNum = handleCookie("get","loginTime") ? parseInt(handleCookie("get","loginTime"),10) + 1 : 1;
                handleCookie("set",'loginTime', totalLoginNum);
                initUpdateDialog();
            }

            // handleCookie("remove","loginTime");
            // handleCookie("remove","pcLastLogin");

        }

    }

    return IE886SDK;

})));
