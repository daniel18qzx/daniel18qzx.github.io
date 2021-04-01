---
title: BeautifulSoup
categories:
  - Python
  - 基本语法
abbrlink: 51103
date: 2019-07-02 00:00:00
---

## 请求


```python
import requests
result = requests.get("https://news.163.com/")
```


```python
# 从返回result的状态码中，了解到是否请求成功
result.status_code
```




    200




```python
result.encoding
```




    'GBK'




```python
content = result.content
print (content[:1000]) #前1000个字符
```

    b' <!DOCTYPE HTML>\n<!--[if IE 6 ]> <html id="ne_wrap" class="ne_ua_ie6 ne_ua_ielte8"> <![endif]-->\n<!--[if IE 7 ]> <html id="ne_wrap" class="ne_ua_ie7 ne_ua_ielte8"> <![endif]-->\n<!--[if IE 8 ]> <html id="ne_wrap" class="ne_ua_ie8 ne_ua_ielte8"> <![endif]-->\n<!--[if IE 9 ]> <html id="ne_wrap" class="ne_ua_ie9"> <![endif]-->\n<!--[if (gte IE 10)|!(IE)]><!--> <html id="ne_wrap" phone="1"> <!--<![endif]-->\n<head>\n<meta http-equiv="Content-Type" content="text/html; charset=utf-8">\n<meta name="model_url" content="http://news.163.com/special/index2015/" />\n<title>\xcd\xf8\xd2\xd7\xd0\xc2\xce\xc5</title>\n<base target="_blank" />\n<meta name="keywords" content="\xd0\xc2\xce\xc5,\xd0\xc2\xce\xc5\xd6\xd0\xd0\xc4,\xd0\xc2\xce\xc5\xc6\xb5\xb5\xc0,\xca\xb1\xca\xc2\xb1\xa8\xb5\xc0" />\n<meta name="description" content="\xd0\xc2\xce\xc5,\xd0\xc2\xce\xc5\xd6\xd0\xd0\xc4,\xb0\xfc\xba\xac\xd3\xd0\xca\xb1\xd5\xfe\xd0\xc2\xce\xc5,\xb9\xfa\xc4\xda\xd0\xc2\xce\xc5,\xb9\xfa\xbc\xca\xd0\xc2\xce\xc5,\xc9\xe7\xbb\xe1\xd0\xc2\xce\xc5,\xca\xb1\xca\xc2\xc6\xc0\xc2\xdb,\xd0\xc2\xce\xc5\xcd\xbc\xc6\xac,\xd0\xc2\xce\xc5\xd7\xa8\xcc\xe2,\xd0\xc2\xce\xc5\xc2\xdb\xcc\xb3,\xbe\xfc\xca\xc2,\xc0\xfa\xca\xb7,\xb5\xc4\xd7\xa8\xd2\xb5\xca\xb1\xca\xc2\xb1\xa8\xb5\xc0\xc3\xc5\xbb\xa7\xcd\xf8\xd5\xbe" />\n  <script type="text/javascript" _keep="true">\n    var matchStr =window.location.href;\n    var reURL = /^(https):\\/\\/.+$/;\n    if(!reURL.test(matchStr)){\n        windo'


## 模拟登入


```python
s = requests.session()
data = {'user':'用户名','passdw':'密码'}
#post 换成登录的地址，
res=s.post('http://www.xxx.net/index.php?action=login',data);
#换成抓取的地址
s.get('http://www.xxx.net/archives/155/');
```

## BeautifulSoup


```python
import warnings
warnings.filterwarnings("ignore")

from bs4 import BeautifulSoup
soup = BeautifulSoup(content, fromEncoding="GB2312") #注意这个地方
print(soup)
```

    <!DOCTYPE HTML>
    <!--[if IE 6 ]> <html id="ne_wrap" class="ne_ua_ie6 ne_ua_ielte8"> <![endif]--><!--[if IE 7 ]> <html id="ne_wrap" class="ne_ua_ie7 ne_ua_ielte8"> <![endif]--><!--[if IE 8 ]> <html id="ne_wrap" class="ne_ua_ie8 ne_ua_ielte8"> <![endif]--><!--[if IE 9 ]> <html id="ne_wrap" class="ne_ua_ie9"> <![endif]--><!--[if (gte IE 10)|!(IE)]><!--><html id="ne_wrap" phone="1"> <!--<![endif]-->
    <head>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
    <meta content="http://news.163.com/special/index2015/" name="model_url"/>
    <title>网易新闻</title>
    <base target="_blank"/>
    <meta content="新闻,新闻中心,新闻频道,时事报道" name="keywords"/>
    <meta content="新闻,新闻中心,包含有时政新闻,国内新闻,国际新闻,社会新闻,时事评论,新闻图片,新闻专题,新闻论坛,军事,历史,的专业时事报道门户网站" name="description"/>
    <script _keep="true" type="text/javascript">
        var matchStr =window.location.href;
        var reURL = /^(https):\/\/.+$/;
        if(!reURL.test(matchStr)){
            window.location.href = "https://news.163.com/";
        }
      </script>
    <!-- 适配3g ie8bug-->
    <!-- 广告样式 -->
    <style>
    .channel_relative_2016{
        position:relative;
        line-height: 0px;
    }
    .channel_relative_2016_lh{
        line-height: 0px;
    }
    .channel_ad_2016{
        height: 17px;
        display:none;
        background: rgba(0,0,0,0.6);
        background: #000\9;
        color: #fff;
        border-radius: 0 8px 0px 0px;
        line-height: 17px;
        width: 30px;
        text-align: left;
        overflow: hidden;
        font-size: 12px;
        font-family: Arial;
        position:absolute;
        left:0;
        bottom:0;
        z-index:3;
    }
    .channel_ad_text_2016{
        position: absolute;
        right: 1px;
        bottom: -2px;
        color: #999999;
        z-index:3;
        font-size: 12px;
        font-family: Arial;
       display:none;
      line-height: 18px;
    }
    .channel_relative_2016 .channel_ad_2016,.channel_relative_2016 .channel_ad_text_2016{
        display: inline-block;
    }
    </style>
    <!-- channel2019_logo样式 -->
    <style type="text/css">
    	.channel2019_logo{
    		background: url(http://cms-bucket.ws.126.net/2019/04/25/09e37a6a4dd349468cd38dd79a3b15b7.png) no-repeat !important;
    		width: 152px !important;
    		height: 37px !important;
    		display: block !important;
    		float: left!important;
    	}
    	/*新闻*/
    	.channel2019_news_logo{
    		background-position: 0px 4px !important;
    	}
    	/*科技*/
    	.channel2019_tech_logo{
    		background-position: 0px -96px !important;
        	
    	}
    	/*手机*/
    	.channel2019_mobile_logo{
    		background-position: 0px -196px !important;
    		
    	}
    	/*数码*/
    	.channel2019_digi_logo{
    		background-position: 0px -296px !important;
        	
    	}
    	/*新闻学院*/
    	.channel2019_college_logo{
    		background-position: 0px -396px !important;
    		width: 213px !important;
    	}
    	/*政务*/
    	.channel2019_gov_logo{
    		background-position: 0px -496px !important;
    	}
    	/*军事*/
    	.channel2019_war_logo{
    		background-position: 0px 0px !important;
        	height: 33px !important;
    	}
    	/*航空*/
    	.channel2019_air_logo{
    		background-position: 0px 0px !important;
        	height: 33px !important;
    	}
       /*新闻排行榜*/
    	.channel2019_newsrank_logo{
    		background-position: 0px 0px !important;
        	height: 33px !important;
    	}
      	/*新闻图片*/
    	.channel2019_newsphoto_logo{
    		background-position: 0px -2200px !important;
          	width: 213px !important;
        	height: 33px !important;
    	}
    	/*体育*/
    	.channel2019_sports_logo{
    		background-position: 0px -796px !important;
    	}
      	/*体育二级页*/
    	.channel2019_sportssub_logo{
    		height: 33px !important;
    		background-position: 0px -800px !important;
    	}
    	/*娱乐*/
    	.channel2019_ent_logo{
    		background-position: 0px -896px !important;
    	}
    	/*音乐*/
    	.channel2019_music_logo{
    		background-position: 0px -900px !important;
        	height: 32px !important;
    	}
    	/*时尚*/
    	.channel2019_fashion_logo{
    		background-position: 0px -1100px !important;
    		height: 32px !important;
    	}
    	/*女人*/
    	.channel2019_lady_logo{
    		background-position: 0px -1196px !important;
    	}
    	/*财经*/
    	.channel2019_money_logo{
    		background-position: 0px -1300px !important;
    	}
        /*手机图片*/
    	.channel2019_mobilephoto_logo{
    		background-position: 0px -2300px !important;
    		width: 213px !important;
        	height: 33px !important;
    	}
    	/*汽车*/
    	.channel2019_auto_logo{
    		background-position: 0px -1396px !important;
    	}
    	/*旅游*/
    	.channel2019_travel_logo{
    		background-position: 0px -1496px !important;
    	}
    	/*健康*/
    	.channel2019_jiankang_logo{
    		background-position: 0px -1596px !important;
    	}
    	/*教育*/
    	.channel2019_edu_logo{
    		background-position: 0px -1696px !important;
    	}
    	/*艺术*/
    	.channel2019_art_logo{
    		background-position: 0px -1796px !important;
    	}
    	/*亲子*/
    	.channel2019_baby_logo{
    		background-position: 0px -1896px !important;
    	}
    	/*双创*/
    	.channel2019_shuangchuang_logo{
    		background-position: 0px -1996px !important;
    	}
    	/*酒香*/
    	.channel2019_jiu_logo{
    		background-position: 0px -2096px !important;
    	}
      	/*游戏*/
    	.channel2019_game_logo{
    		background-position: 0px -2400px !important;
    	}
    	</style>
    <script _keep="true" type="text/javascript">
    (function() {
        if(/s=noRedirect/i.test(location.search)) return; 
        if(/AppleWebKit.*Mobile/i.test(navigator.userAgent) || (/MIDP|SymbianOS|NOKIA|SAMSUNG|LG|NEC|TCL|Alcatel|BIRD|DBTEL|Dopod|PHILIPS|HAIER|LENOVO|MOT-|Nokia|SonyEricsson|SIE-|Amoi|ZTE/.test(navigator.userAgent))) {
            try {
                if(/Android|Windows Phone|webOS|iPhone|iPod|BlackBerry/i.test(navigator.userAgent)) {
                     window.location.href = "https://3g.163.com/touch/news/";
                } else if(/iPad/i.test(navigator.userAgent)) {
                    window.location.href = "https://news.163.com/pad/"
                }
            } catch(e) {}
        }   
    })();
    </script>
    <script _keep="true" charset="gbk" src="//news.163.com/special/00015CJL/xw_news_data.js"></script>
    <!-- 社交传播统计 -->
    <script src="//static.ws.126.net/163/frontend/libs/antanalysis.min.js"></script>
    <script _keep="true" src="//static.ws.126.net/163/frontend/antnest/NTM-KFGT6I8U-38.js"></script>
    <script crossorigin="anonymous" src="https://static.ws.126.net/163/frontend/libs/raven-3.26.2.min.js"></script>
    <link href="https://static.ws.126.net/163/f2e/news/index2016_rmd/css/head~a2a2093f5d52d.css" rel="stylesheet"/>
    </head>
    <body class="news_pc" ne-class="{{myState.isNs9 ? 'ns9' : 'ns12'}}" ne-module="/news/index2016_rmd/index2016.js">
    <div class="index2016_wrap" id="index2016_wrap">
    <div>
    <!-- 节日动画 start -->
    <!-- 节日动画 end -->
    <div class="common_nav">
    <link href="//static.ws.126.net/163/f2e/commonnav2019/css/commonnav_headcss-61ce66f60e.css" rel="stylesheet"/>
    <!-- urs -->
    <script _keep="true" src="//urswebzj.nosdn.127.net/webzj_cdn101/message.js" type="text/javascript"></script>
    <div class="ntes_nav_wrap" id="js_N_NTES_wrap">
    <div class="ntes-nav" id="js_N_nav">
    <div class="ntes-nav-main clearfix">
    <div class="c-fl">
    <a class="ntes-nav-index-title ntes-nav-entry-wide c-fl" href="http://www.163.com/" title="网易首页">网易首页</a>
    <!-- 应用 -->
    <div class="js_N_navSelect ntes-nav-select ntes-nav-select-wide ntes-nav-app c-fl">
    <a class="ntes-nav-select-title ntes-nav-entry-bgblack JS_NTES_LOG_FE" href="http://www.163.com/#f=topnav">应用
                <em class="ntes-nav-select-arr"></em>
    </a>
    <div class="ntes-nav-select-pop">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="http://m.163.com/newsapp/#f=topnav">
    <span>
    <em class="ntes-nav-app-newsapp">网易新闻</em>
    </span>
    </a>
    </li>
    <li>
    <a href="http://open.163.com/#f=topnav">
    <span>
    <em class="ntes-nav-app-open">网易公开课</em>
    </span>
    </a>
    </li>
    <li>
    <a href="https://hongcai.163.com/?from=pcsy-button">
    <span>
    <em class="ntes-nav-app-hongcai">网易红彩</em>
    </span>
    </a>
    </li>
    <li>
    <a href="http://u.163.com/aosoutbdbd8">
    <span>
    <em class="ntes-nav-app-yanxuan">网易严选</em>
    </span>
    </a>
    </li>
    <li>
    <a href="http://mail.163.com/client/dl.html?from=mail46">
    <span>
    <em class="ntes-nav-app-mail">邮箱大师</em>
    </span>
    </a>
    </li>
    <li>
    <a href="http://study.163.com/client/download.htm?from=163app&amp;utm_source=163.com&amp;utm_medium=web_app&amp;utm_campaign=business">
    <span>
    <em class="ntes-nav-app-study">网易云课堂</em>
    </span>
    </a>
    </li>
    <li class="last">
    <a href="http://da.kaola.com/redirect?t=5aaebece47f92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=6b69bfbfac0db5f335232faa957a27bb&amp;target=https%3A%2F%2Fapp.kaola.com%2F%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>
    <em class="ntes-nav-app-kaola-hg">网易考拉</em>
    </span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </div>
    <div class="c-fr">
    <!-- 片段开始 -->
    <div class="ntes-nav-quick-navigation">
    <a class="ntes-nav-quick-navigation-btn" href="javascript:void(0);" id="js_N_ntes_nav_quick_navigation_btn" target="_self">
    <em>快速导航
                  <span class="menu1"></span>
    <span class="menu2"></span>
    <span class="menu3"></span>
    </em>
    </a>
    <div class="ntes-quicknav-pop" id="js_N_ntes_quicknav_pop">
    <div class="ntes-quicknav-list">
    <div class="ntes-quicknav-content">
    <ul class="ntes-quicknav-column ntes-quicknav-column-1">
    <li>
    <h3><a href="https://news.163.com">新闻</a></h3>
    </li>
    <li>
    <a href="http://news.163.com/domestic">国内</a>
    </li>
    <li>
    <a href="http://news.163.com/world">国际</a>
    </li>
    <li>
    <a href="http://news.163.com/photo">图片</a>
    </li>
    <li>
    <a href="http://view.163.com">评论</a>
    </li>
    <li>
    <a href="http://discovery.163.com">探索</a>
    </li>
    <li>
    <a href="http://war.163.com">军事</a>
    </li>
    <li>
    <a href="http://news.163.com/localnews/">本地新闻</a>
    </li>
    <li>
    <a href="http://news.163.com/special/wangsansanhome/">王三三</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-2">
    <li>
    <h3><a href="http://sports.163.com">体育</a></h3>
    </li>
    <li>
    <a href="http://sports.163.com/nba">NBA</a>
    </li>
    <li>
    <a href="http://sports.163.com/cba">CBA</a>
    </li>
    <li>
    <a href="http://sports.163.com/allsports">综合</a>
    </li>
    <li>
    <a href="http://sports.163.com/zc">中超</a>
    </li>
    <li>
    <a href="http://sports.163.com/world">国际足球</a>
    </li>
    <li>
    <a href="http://sports.163.com/yc">英超</a>
    </li>
    <li>
    <a href="http://sports.163.com/xj">西甲</a>
    </li>
    <li>
    <a href="http://sports.163.com/yj">意甲</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-3">
    <li>
    <h3><a href="http://ent.163.com">娱乐</a></h3>
    </li>
    <li>
    <a href="http://ent.163.com/star">明星</a>
    </li>
    <li>
    <a href="http://ent.163.com/photo">图片</a>
    </li>
    <li>
    <a href="http://ent.163.com/movie">电影</a>
    </li>
    <li>
    <a href="http://ent.163.com/tv">电视</a>
    </li>
    <li>
    <a href="http://ent.163.com/music">音乐</a>
    </li>
    <li>
    <a href="http://ent.163.com/special/gsbjb/">稿事编辑部</a>
    </li>
    <li>
    <a href="http://ent.163.com/special/focus_ent/">娱乐FOCUS</a>
    </li>
    <li><a href="http://ent.163.com/special/xbkhz/">星捕快</a></li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-4">
    <li>
    <h3><a href="http://money.163.com">财经</a></h3>
    </li>
    <li>
    <a href="http://money.163.com/stock">股票</a>
    </li>
    <li>
    <a href="http://quotes.money.163.com/stock">行情</a>
    </li>
    <li>
    <a href="http://money.163.com/chanjing">产经</a>
    </li>
    <li>
    <a href="http://money.163.com/ipo">新股</a>
    </li>
    <li>
    <a href="http://money.163.com/finance">金融</a>
    </li>
    <li>
    <a href="http://money.163.com/fund">基金</a>
    </li>
    <li>
    <a href="http://biz.163.com">商业</a>
    </li>
    <li>
    <a href="http://money.163.com/licai">理财</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-5">
    <li>
    <h3><a href="http://auto.163.com">汽车</a></h3>
    </li>
    <li>
    <a href="http://auto.163.com/buy">购车</a>
    </li>
    <li>
    <a href="http://auto.163.com/depreciate">行情</a>
    </li>
    <li>
    <a href="http://product.auto.163.com/finder">选车</a>
    </li>
    <li>
    <a href="http://product.auto.163.com">车型库</a>
    </li>
    <li>
    <a href="http://auto.163.com/news">行业</a>
    </li>
    <li>
    <a href="http://auto.163.com/chezhu">用车</a>
    </li>
    <li>
    <a href="http://auto.163.com/photo">汽车图片</a>
    </li>
    <li>
                       
                      </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-6">
    <li>
    <h3><a href="http://tech.163.com">科技</a></h3>
    </li>
    <li>
    <a href="http://tech.163.com/telecom/">通信</a>
    </li>
    <li>
    <a href="http://tech.163.com/it">IT</a>
    </li>
    <li>
    <a href="http://tech.163.com/internet">互联网</a>
    </li>
    <li>
    <a href="http://tech.163.com/special/ydhlw">移动互联网</a>
    </li>
    <li>
    <a href="http://tech.163.com/special/chzt">特别策划</a>
    </li>
    <li>
    <a href="http://tech.163.com/special/wudaokou">五道口沙龙</a>
    </li>
    <li>
    <a href="http://tech.163.com/special/yyzd">易语中的</a>
    </li>
    <li>
    <a href="http://tech.163.com/special">专题</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-7">
    <li>
    <h3><a href="http://lady.163.com">女人</a></h3>
    </li>
    <li>
    <a href="http://baby.163.com">亲子</a>
    </li>
    <li>
    <a href="http://fashion.163.com/art">艺术</a>
    </li>
    <li>
    <a href="http://fashion.163.com">时尚</a>
    </li>
    <li>
    <a href="http://shoucang.163.com">收藏</a>
    </li>
    <li>
    <a href="http://lady.163.com/sense">情感</a>
    </li>
    <li>
    <a href="http://lady.163.com/astro">星座</a>
    </li>
    <li>
    <a href="http://lady.163.com/beauty">美容</a>
    </li>
    <li>
    <a href="http://cosmetic.lady.163.com/trial">免费试用</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-8">
    <li>
    <h3><a href="http://mobile.163.com">手机</a><span>/</span><a href="http://digi.163.com/">数码</a></h3>
    </li>
    <li>
    <a href="http://mobile.163.com/mi">移动</a>
    </li>
    <li>
    <a href="http://digi.163.com/pc">电脑</a>
    </li>
    <li>
    <a href="http://product.mobile.163.com">手机库</a>
    </li>
    <li>
    <a href="http://hea.163.com/">家电</a>
    </li>
    <li>
    <a href="http://digi.163.com/smart">智能硬件</a>
    </li>
    <li>
    <a href="http://digi.163.com/dc">相机</a>
    </li>
    <li>
    <a href="http://v.mobile.163.com">手机视频</a>
    </li>
    <li>
                       
                      </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-9">
    <li>
    <h3><a href="http://house.163.com">房产</a><span>/</span><a href="http://home.163.com">家居</a></h3>
    </li>
    <li>
    <a href="http://bj.house.163.com">北京房产</a>
    </li>
    <li>
    <a href="http://sh.house.163.com">上海房产</a>
    </li>
    <li>
    <a href="http://gz.house.163.com">广州房产</a>
    </li>
    <li>
    <a href="http://house.163.com/city">全部分站</a>
    </li>
    <li>
    <a href="http://xf.house.163.com">楼盘库</a>
    </li>
    <li>
    <a href="http://home.163.com/jiaju/">家具</a>
    </li>
    <li>
    <a href="http://home.163.com/weiyu/">卫浴</a>
    </li>
    <li>
    <a href="http://home.163.com/special/jiajuyigui">衣柜</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-10">
    <li>
    <h3><a href="http://travel.163.com">旅游</a></h3>
    </li>
    <li>
    <a href="http://travel.163.com/outdoor">户外</a>
    </li>
    <li>
    <a href="http://guizhou.travel.163.com">贵州</a>
    </li>
    <li>
    <a href="http://travel.163.com/food">美食</a>
    </li>
    <li>
    <a href="http://jingdian.travel.163.com/domestic/1000066937">四川</a>
    </li>
    <li>
    <a href="http://jingdian.travel.163.com">景点</a>
    </li>
    <li>
    <a href="http://jingdian.travel.163.com/domestic/1000066944">新疆</a>
    </li>
    <li>
    <a href="http://travel.163.com/special/travellist/#f=endnav">专题</a>
    </li>
    <li>
    <a href="http://jingdian.travel.163.com/domestic/1000066926/#f=endnav">西藏</a>
    </li>
    </ul>
    <ul class="ntes-quicknav-column ntes-quicknav-column-11">
    <li>
    <h3><a href="http://edu.163.com">教育</a></h3>
    </li>
    <li>
    <a href="http://edu.163.com/yimin">移民</a>
    </li>
    <li>
    <a href="http://edu.163.com/kaoyan">考研</a>
    </li>
    <li>
    <a href="http://edu.163.com/liuxue">留学</a>
    </li>
    <li>
    <a href="http://edu.163.com/special/official">公务员</a>
    </li>
    <li>
    <a href="http://edu.163.com/en">外语</a>
    </li>
    <li>
    <a href="http://kids.163.com">中小学</a>
    </li>
    <li>
    <a href="http://edu.163.com/gaokao">高考</a>
    </li>
    <li>
    <a href="http://daxue.163.com">校园</a>
    </li>
    </ul>
    <div class="ntes-nav-sitemap"><a href="http://sitemap.163.com/"><i></i>查看网易地图</a></div>
    </div>
    </div>
    </div>
    </div>
    <div class="c-fr">
    <div class="c-fl" id="js_N_navLoginBefore">
    <div class="js_loginframe ntes-nav-login ntes-nav-login-normal" id="js_N_navHighlight">
    <a class="ntes-nav-login-title" href="http://reg.163.com/" id="js_N_nav_login_title">登录</a>
    <div class="ntes-nav-loginframe-pop" id="js_N_login_wrap">
    <!--加载登陆组件-->
    </div>
    </div>
    <div class="js_N_navSelect ntes-nav-select ntes-nav-select-wide JS_NTES_LOG_FE c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-register" href="http://reg.email.163.com/mailregAll/reg0.jsp?from=163navi&amp;regPage=163">注册免费邮箱
                    <em class="ntes-nav-select-arr"></em>
    </a>
    <div class="ntes-nav-select-pop">
    <ul class="ntes-nav-select-list clearfix" style="width:210px;">
    <li>
    <a href="http://reg.vip.163.com/register.m?from=topnav">
    <span style="width:190px;">注册VIP邮箱（特权邮箱，付费）</span>
    </a>
    </li>
    <li class="last JS_NTES_LOG_FE">
    <a href="http://mail.163.com/client/dl.html?from=mail46">
    <span style="width:190px;">免费下载网易官方手机邮箱应用</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </div>
    <div class="c-fl" id="js_N_navLoginAfter" style="display:none">
    <div class="js_N_navSelect ntes-nav-select ntes-nav-logined JS_NTES_LOG_FE" id="js_N_logined_warp">
    <span class="ntes-nav-select-title ntes-nav-logined-userinfo">
    <span class="ntes-nav-logined-username" id="js_N_navUsername"></span>
    <em class="ntes-nav-select-arr"></em>
    </span>
    <div class="ntes-nav-select-pop" id="js_login_suggest_wrap">
    <ul class="ntes-nav-select-list clearfix" id="js_logined_suggest"></ul>
    </div>
    </div>
    <a class="ntes-nav-entry-wide c-fl" id="js_N_navLogout" target="_self">安全退出</a>
    </div>
    </div>
    <ul class="ntes-nav-inside">
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-mobile-title ntes-nav-entry-bgblack" href="http://www.163.com/newsapp/#f=163nav">
    <em class="ntes-nav-entry-mobile">移动端</em>
    </a>
    <div class="qrcode-img">
    <a href="http://www.163.com/newsapp/#f=163nav">
    <img src="//static.ws.126.net/f2e/include/common_nav/images/topapp.jpg"/>
    </a>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-huatian ntes-nav-entry-bgblack" href="https://open.163.com/" id="js_love_url">
    <em class="ntes-nav-entry-huatian">网易公开课</em>
    <em class="ntes-nav-select-arr"></em>
    <span class="ntes-nav-msg">
    <em class="ntes-nav-msg-num"></em>
    </span>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-huatian">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="https://vip.open.163.com">
    <span>付费精品</span>
    </a>
    </li>
    <li>
    <a href="https://open.163.com/ted/">
    <span>TED</span>
    </a>
    </li>
    <li>
    <a href="https://open.163.com/ocw/">
    <span>国际名校公开课</span>
    </a>
    </li>
    <li>
    <a href="http://open.163.com/cuvocw/">
    <span>中国大学视频公开课</span>
    </a>
    </li>
    <li>
    <a href="https://open.163.com/appreciation">
    <span>赏课</span>
    </a>
    </li>
    <li>
    <a href="https://open.163.com/khan/">
    <span>可汗学院</span>
    </a>
    </li>
    <li class="last">
    <a href="http://open.163.com/special/appdownload_pc/">
    <span>下载公开课</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-kaola ntes-nav-entry-bgblack" href="http://da.kaola.com/redirect?t=5aaebece48792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=d638f275b1755320e845734e53e897ee&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505" id="js_kaola_url">
    <em class="ntes-nav-entry-kaola">网易考拉</em>
    <em class="ntes-nav-select-arr"></em>
    <span class="ntes-nav-msg ntes-nav-kaola-msg" id="js_N_navKaolaMsg">
    <em class="ntes-nav-msg-num"></em>
    </span>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-kaola">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece48f92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=b3e224752b2cad85e9831e8c6cf7fbbd&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fbimaibangdan.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>1000元新人大礼包</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece49392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=fd8e43f4a20a26fbe60f7e7de1f17efe&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>新人专享进口好货</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece49392c01&amp;p=c901ea7c&amp;proId=1024&amp;code=21bcd5b595fc235cfd11e3e1cff14177&amp;target=https%3A%2F%2Factivity.kaola.com%2Factivity%2FflashSaleIndex%2Fshow.html%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>今日限时抢购</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece49792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=ecc40777cb2d68a3d9fb078b232f081d&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfyrzolcpagerz.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>营养保健</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece49b92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=0cdd5a920c768340ffc12eccd659341d&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fnewpc.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>个人洗护</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece4a392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=ee49a3a793f22e648ac616f5dab061dd&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjpwmb9zcpagesl.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>美容彩妆</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece4a792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=6eb2598fd20963efc203a4e3fe88f4e2&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fmyxrq.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>母婴儿童</span>
    </a>
    </li>
    <li>
    <a href="http://da.kaola.com/redirect?t=5aaebece4ab92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=3946ce460ba655c11afac69855dfc02b&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Ffoodnewcustomers.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>环球美食</span>
    </a>
    </li>
    <li class="last">
    <a href="http://da.kaola.com/redirect?t=5aaebece4af92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=2eee7290051863737a434d44f3c0d46f&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fnewtalent.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>家居生活</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-lofter ntes-nav-entry-bgblack" href="http://you.163.com/?from=web_fc_menhu_xinrukou_1" id="js_lofter_icon_url">
    <em class="ntes-nav-entry-lofter">网易严选</em>
    <em class="ntes-nav-select-arr"></em>
    <span class="ntes-nav-msg" id="js_N_navLofterMsg">
    <em class="ntes-nav-msg-num"></em>
    </span>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-lofter">
    <ul class="ntes-nav-select-list clearfix" id="js_lofter_pop_url">
    <li>
    <a href="http://you.163.com/act/static/Fb2d1OZ714.html?from=web_fc_menhu_xinrukou_1">
    <span>888元现金券</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/manufacturer/list?from=web_fc_menhu_xinrukou_3">
    <span>品牌制造商爆款</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/item/recommend?from=web_fc_menhu_xinrukou_4">
    <span>999+人气好评品</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/flashSale/index?from=web_fc_menhu_xinrukou_5">
    <span>限时特惠</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/item/list?categoryId=1005000&amp;from=web_fc_menhu_xinrukou_7">
    <span>居家床品</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/item/list?categoryId=1005001&amp;from=web_fc_menhu_xinrukou_8">
    <span>精致餐厨</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/item/list?categoryId=1008000&amp;from=web_fc_menhu_xinrukou_9">
    <span>箱包鞋类</span>
    </a>
    </li>
    <li>
    <a href="http://you.163.com/item/list?categoryId=1010000&amp;from=web_fc_menhu_xinrukou_10">
    <span>经典服饰</span>
    </a>
    </li>
    <li class="last">
    <a href="http://you.163.com/item/list?categoryId=1005002&amp;from=web_fc_menhu_xinrukou_11">
    <span>健康美食</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-money ntes-nav-entry-bgblack" href="http://pay.163.com/">
    <em class="ntes-nav-entry-money">支付</em>
    <em class="ntes-nav-select-arr"></em>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-temp">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="http://pay.163.com/#f=topnav">
    <span>一卡通充值</span>
    </a>
    </li>
    <li>
    <a href="http://ecard.163.com/script/index#f=topnav">
    <span>一卡通购买</span>
    </a>
    </li>
    <li>
    <a href="https://k.163.com/?product=163&amp;trackid=01">
    <span>网易白金卡</span>
    </a>
    </li>
    <li>
    <a href="https://epay.163.com/">
    <span>我的网易支付</span>
    </a>
    </li>
    <li>
    <a href="https://3c.163.com/?from=wangyimenhu16">
    <span>网易智造</span>
    </a>
    </li>
    <li class="last">
    <a href="http://lq.163.com?from=neteasemoney">
    <span>网易来钱-借现金</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-cart ntes-nav-entry-bgblack" href="http://baoxian.163.com/car/?from=mhgwc">
    <em class="ntes-nav-entry-cart">电商</em>
    <em class="ntes-nav-select-arr"></em>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-temp">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="http://you.163.com?from=web_in_wydaohang">
    <span>严选</span>
    </a>
    </li>
    <li>
    <a href="http://lq.163.com?from=neteasebuy">
    <span>我要借钱</span>
    </a>
    </li>
    <li class="last">
    <a href="http://da.kaola.com/redirect?t=5aaebece4b392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=d15f8f9d72ccc507aeefda91b43c0cd2&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
    <span>网易考拉</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    <li>
    <div class="js_N_navSelect ntes-nav-select c-fl">
    <a class="ntes-nav-select-title ntes-nav-select-title-mail ntes-nav-entry-bgblack" id="js_mail_url">
    <em class="ntes-nav-entry-mail">邮箱</em>
    <em class="ntes-nav-select-arr"></em>
    <span class="ntes-nav-msg" id="js_N_navMailMsg">
    <em class="ntes-nav-msg-num" id="js_N_navMailMsgNum"></em>
    </span>
    </a>
    <div class="ntes-nav-select-pop ntes-nav-select-pop-mail">
    <ul class="ntes-nav-select-list clearfix">
    <li>
    <a href="http://email.163.com/#f=topnav">
    <span>免费邮箱</span>
    </a>
    </li>
    <li>
    <a href="http://vipmail.163.com/#f=topnav">
    <span>VIP邮箱</span>
    </a>
    </li>
    <li>
    <a href="http://qiye.163.com/#f=topnav">
    <span>企业邮箱</span>
    </a>
    </li>
    <li>
    <a href="http://reg.email.163.com/mailregAll/reg0.jsp?from=ntes_nav&amp;regPage=163">
    <span>免费注册</span>
    </a>
    </li>
    <li>
    <a href="http://reg.email.163.com/unireg/call.do?cmd=register.entrance&amp;flow=mobile&amp;from=ntes_nav">
    <span>快速注册</span>
    </a>
    </li>
    <li class="last">
    <a href="http://mail.163.com/dashi/dlpro.html?from=mail46">
    <span>客户端下载</span>
    </a>
    </li>
    </ul>
    </div>
    </div>
    </li>
    </ul>
    </div>
    </div>
    </div>
    </div>
    <script src="//static.ws.126.net/163/f2e/commonnav2019/js/commonnav_headjs-2f356198e6.js"></script>
    </div>
    <!-- 节日背景 -->
    <div class="ns-bg-wrap">
    <div class="N-nav-channel JS_NTES_LOG_FE" data-module-name="xwwzy_11_headdaohang">
    <a class="first" href="https://news.163.com/">新闻</a><a href="http://sports.163.com/">体育</a><a href="http://sports.163.com/nba/">NBA</a><a href="http://ent.163.com/">娱乐</a><a href="http://money.163.com/">财经</a><a href="http://money.163.com/stock/">股票</a><a href="http://auto.163.com/" id="_link_auto">汽车</a><a href="http://tech.163.com/">科技</a><a href="http://mobile.163.com/">手机</a><a href="http://digi.163.com/">数码</a><a href="http://lady.163.com/">女人</a><a href="http://v.163.com/">直播</a><a href="http://v.163.com/special/video/#tuijian">视频</a><a href="http://travel.163.com/">旅游</a><a href="http://house.163.com/" id="houseUrl">房产</a><a href="http://home.163.com/" id="homeUrl">家居</a><a href="http://edu.163.com/">教育</a><a href="http://book.163.com/">读书</a><a href="https://news.163.com/" id="_link_game">本地</a><a href="http://jiankang.163.com/">健康</a><a href="http://rd.da.netease.com/redirect?t=5802fb18cf033c80&amp;p=e17af55c&amp;proId=1024&amp;target=https%3A%2F%2Fwww.kaola.com%2F%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">海淘</a><a class="last" href="http://art.163.com/">艺术</a>
    </div>
    <!-- 游戏替换为本地，并定向 0310-->
    <!-- 配置定向城市 -->
    <script _keep="true" type="text/javascript">
    var HouseNavBendiTxt = {
        "province": [
            {
                "name": "北京市",
                "shortName": "北京",
                "url":"http://bj.news.163.com/"
            },
            {
                "name": "上海市",
                "shortName": "上海",
                "url":"http://sh.news.163.com/"
            },
            {
                "name": "天津市",
                "shortName": "天津",
                "url":"http://tj.news.163.com/"
            },
            {
                "name": "广东省",
                "shortName": "广东",
                "url":"http://gd.news.163.com/"
            },
            {
                "name": "江苏省",
                "shortName": "江苏",
                "url":"http://js.news.163.com/"
            },
            {
                "name": "浙江省",
                "shortName": "浙江",
                "url":"http://zj.news.163.com/"
            },
            {
                "name": "四川省",
                "shortName": "四川",
                "url":"http://sc.news.163.com/"
            },
            {
                "name": "黑龙江省",
                "shortName": "黑龙江",
                "url":"http://hlj.news.163.com/"
            },
            {
                "name": "吉林省",
                "shortName": "吉林",
                "url":"http://jl.news.163.com/"
            },
            {
                "name": "辽宁省",
                "shortName": "辽宁",
                "url":"http://liaoning.news.163.com/"
            },
            {
                "name": "内蒙古自治区",
                "shortName": "内蒙古",
                "url":"http://hhht.news.163.com/"
            },
            {
                "name": "河北省",
                "shortName": "河北",
                "url":"http://hebei.news.163.com/"
            },
            {
                "name": "河南省",
                "shortName": "河南",
                "url":"http://henan.163.com/"
            },
            {
                "name": "山东省",
                "shortName": "山东",
                "url":"http://sd.news.163.com/"
            },
            {
                "name": "陕西省",
                "shortName": "陕西",
                "url":"http://shanxi.news.163.com/"
            },
            {
                "name": "甘肃省",
                "shortName": "甘肃",
                "url":"http://gs.news.163.com/"
            },
            {
                "name": "宁夏回族自治区",
                "shortName": "宁夏",
                "url":"http://ningxia.news.163.com/"
            },
            {
                "name": "新疆维吾尔自治区",
                "shortName": "新疆",
                "url":"http://xj.news.163.com/"
            },
            {
                "name": "安徽省",
                "shortName": "安徽",
                "url":"http://ah.news.163.com/"
            },
            {
                "name": "福建省",
                "shortName": "福建",
                "url":"http://fj.news.163.com/"
            },
            {
                "name": "广西壮族自治区",
                "shortName": "广西",
                "url":"http://gx.news.163.com/"
            },
            {
                "name": "重庆市",
                "shortName": "重庆",
                "url":"http://chongqing.163.com/"
            },
            {
                "name": "湖北省",
                "shortName": "湖北",
                "url":"http://hb.news.163.com/"
            },
            {
                "name": "江西省",
                "shortName": "江西",
                "url":"http://jx.news.163.com/"
            },
            {
                "name": "海南省",
                "shortName": "海南",
                "url":"http://hn.news.163.com/"
            },
            {
                "name": "贵州省",
                "shortName": "贵州",
                "url":"http://gz.news.163.com/"
            },
            {
                "name": "云南省",
                "shortName": "云南",
                "url":"http://yn.news.163.com/"
            },
            {
                "name": "湖南省",
                "shortName": "上海",
                "url":"http://sh.news.163.com/"
            },
            {
                "name": "山西省",
                "shortName": "山西",
                "url":"http://sx.news.163.com"
            },
            {
                "name": "西藏自治区",
                "shortName": "北京",
                "url":"http://bj.news.163.com/"
            },
            {
                "name": "香港特别行政区",
                "shortName": "广东",
                "url":"http://gd.news.163.com/"
            },
            {
                "name": "澳门特别行政区",
                "shortName": "广东",
                "url":"http://gd.news.163.com/"
            },
            {
                "name": "台湾省",
                "shortName": "广东",
                "url":"http://gd.news.163.com/"
            },
            {
                "name": "天津市",
                "shortName": "北京",
                "url":"http://bj.news.163.com/"
            },
            {
                "name": "青海省",
                "shortName": "北京",
                "url":"http://bj.news.163.com/"
            }
        ],
        "city": [
            {
                "name": "大连市",
                "shortName": "大连",
                "url":"http://dl.news.163.com"
            },
            {
                "name": "青岛市",
                "shortName": "青岛",
                "url":"http://qingdao.news.163.com"
            },
            {
                "name": "宁波市",
                "shortName": "宁波",
                "url":"http://ningbo.news.163.com"
            },
            {
                "name": "厦门市",
                "shortName": "厦门",
                "url":"http://xiamen.news.163.com"
            },
            {
                "name": "深圳市",
                "shortName": "深圳",
                "url":"http://shenzhen.news.163.com/"
            }
        ],
        "defalt": {
                "name": "",
                "shortName": "本地",
                "url":"http://news.163.com/"
            }
    };
    </script>
    <script _keep="true" type="text/javascript">
        //本地设置定向省份
        function setBendiName(){
            var js_nav_bendi = document.getElementById("_link_game");
            var cityname = "";
            var cityurl = "";
            var _loc = window.localAddress;
            if(!js_nav_bendi)
                return;
            if(HouseNavBendiTxt.city && _loc){
                var citylist = HouseNavBendiTxt.city;
                var localcity = _loc.city;
                for(var i=0;i<citylist.length;i++){
                    if(citylist[i].name == localcity){
                        cityname = citylist[i].shortName;
                        cityurl = citylist[i].url;
                        break;
                    }
                }
            }
            if(cityname == "" && cityurl == "" && HouseNavBendiTxt.province && _loc){
                var provincelist = HouseNavBendiTxt.province;
                var localprovince = _loc.province;
                for(var i=0;i<provincelist.length;i++){
                    if(provincelist[i].name == localprovince){
                        cityname = provincelist[i].shortName;
                        cityurl = provincelist[i].url;
                        break;
                    }
                }
            }
            if(js_nav_bendi && cityname != "" && cityurl != ""){
                js_nav_bendi.innerHTML = cityname;
                js_nav_bendi.href = cityurl;
            }
            if(js_nav_bendi && cityname == "" && cityurl == ""){
                js_nav_bendi.innerHTML = "本地";
                js_nav_bendi.href = "http://news.163.com";
            }
        }
        function BENDI_NAV_CALLBACK(data){
           if(data && data.result){
                if(window.HouseNavBendiTxt){
                    window.localAddress = data.result;
                    setBendiName();
                } 
           }
        };
        
        if(window.localAddress){
            if(window.HouseNavBendiTxt){
                setBendiName();
            } 
        }else{
            var url = "//ipservice.163.com/locate/api/getLocByIp?key=C6E22B7D480E3312C74EC7EF013E50C5&callback=BENDI_NAV_CALLBACK";
            var script = document.createElement('script');
            script.setAttribute('src', url);
            document.getElementsByTagName('head')[0].appendChild(script);
        }
    </script>
    <div class="index2016_content">
    <!-- 头部广告 开始-->
    <div class="ns_area index_top_ad channel_relative_2016">
    <!--16新闻首页顶通-->
    <div adtype="topColumnAd" class="at_item common_ad_item top_ad_column" requesturl="https://nex.163.com/q?app=7BE0FC82&amp;c=news&amp;l=11&amp;site=netease&amp;affiliate=news&amp;cat=homepage&amp;type=column1200x125_960x100&amp;location=10"></div>
    <span class="channel_ad_2016">广告</span>
    </div>
    <!-- 头部广告 结束-->
    <!-- 头部导航 开始-->
    <div class="index_head">
    <div ne-module="/news/index2016_rmd/modules/head/head.js">
    <div class="ns_area hd">
    <h1>
    <a class="channel2019_logo channel2019_news_logo" href="https://news.163.com/">网易新闻有态度</a>
    </h1>
    <!-- <div class="top-search">
            <form action="http://news.yodao.com/search" method="get" name="nisearch_top" id="formtop" target="_blank">
                <input type="hidden" name="keyfrom" value="sports.163">
                <input type="hidden" name="suser" value="user163">
                <input type="hidden" name="ue" value="gbk">
                <div class="search-input"> <span class="hidden">搜索</span>
                    <input type="text" name="q" id="searchInput_top" onfocus="this.value=''" value="输入关键字" class="text-box ">
                    <input type="submit" name="Submit" value="" tabindex="0" title="搜索" class="search-submit" id="sb_form_go">
                </div>
            </form>
        </div> -->
    <!-- 天气 -->
    <div class="ns-lid-weather" id="nsWeatherTop">
    <div class="ns-weather" id="nsWeather">
    <a href="http://news.163.com/weather/">
    <script ne-repeat="weather in weatherInfo" type="text/template">
                    <img class="ns-weather-icon" ne-src="http://static.ws.126.net/f2e/news/index2015/img/weather/<%=weather.icon%>">
                    <div class="ns-weather-text"><%=weather.weather%></div>
                    <div class="ns-weather-info"><%=weather.temp2%>°~<%=weather.temp1%>°</div>
                    <div class="ns-weather-city"><%=weather.city%></div>
                </script>
    </a>
    </div>
    </div>
    </div>
    </div>
    <div class="bd">
    <div class="ns_area list">
    <ul>
    <li class="first"><a href="http://www.163.com/">首页</a></li>
    <li><a href="http://news.163.com/rank/">排行</a></li>
    <li><a href="http://news.163.com/photo/#Current">图片</a></li>
    <li class="menu_guonei"><a href="http://news.163.com/domestic/">国内</a></li>
    <li class="menu_guoji"><a href="http://news.163.com/world/">国际</a></li>
    <!--<li class="menu_shehui"><a href="http://news.163.com/shehui/">社会</a></li>-->
    <li><a href="http://data.163.com/special/datablog/">数读</a></li>
    <li class="menu_war"><a href="http://war.163.com/">军事</a></li>
    <li class="menu_hangkong"><a href="http://news.163.com/air/">航空</a></li>
    <li class="menu_wurenji"><a href="http://news.163.com/uav/">无人机</a></li>
    <li><a href="http://news.163.com/college">新闻学院</a></li>
    <li><a href="http://gov.163.com/">政务</a></li>
    <li><a href="http://gongyi.163.com/">公益</a></li>
    <li><a href="http://media.163.com/">媒体</a></li>
    <li class="last"><a href="http://news.163.com/special/wangsansanhome/">王三三</a></li>
    </ul>
    </div>
    </div>
    </div>
    <!-- 头部导航 结束-->
    <!-- 内容区域 开始 -->
    <div class="ns_area clearfix index_main">
    <!-- 原创栏目 开始 -->
    <div class="main_origina_column" id="js_origina_column">
    <div ne-module="/news/index2016_rmd/modules/originacolumn/originacolumn.js">
    <div class="origina_column_warp">
    <h2>
    <span>新闻各有态度</span>
    </h2>
    <div class="scroll_bd" ne-role="scroll_bd">
    <div class="scroll_column_bd">
    <ul class="scroll_ul">
    <!-- 回声 开始 -->
    <!-- 回声 结束 -->
    <!-- 数读 开始 -->
    <li class="cell cell_sd cell_hover">
    <p class="tag_line">
    <a class="tags tag_sd" href="http://data.163.com/special/datablog/">数读</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://data.163.com/19/0626/14/EIJQJG9L000181IU.html" ne-role="detail">
    <h3>
                                    中国哪里的地铁最拥挤？
                                </h3>
    <div class="photo">
    <img alt="中国哪里的地铁最拥挤？" height="90" src="https://cms-bucket.ws.126.net/2019/06/26/30e8760df3044e29a18fac3514dd22b1.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://data.163.com/19/0625/11/EIH0CQEK00019GOE.html">娶一个潮汕老婆到底是什么体验</a></li>
    <li class="twoli"><a href="http://data.163.com/19/0621/17/EI7BLS3600019GOE.html">不瞒你说，成都早餐好吃到爆</a></li>
    </ul>
    </div>
    </li>
    <!-- 数读 结束 -->
    <!-- 人间 开始 -->
    <li class="cell cell_rj">
    <p class="tag_line">
    <a class="tags tag_rj" href="http://renjian.163.com/">人间</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0628/14/EIP21K41000181RV.html" ne-role="detail">
    <h3>
                                    小白作者的变现之路
                                </h3>
    <div class="photo">
    <img alt="小白作者的变现之路" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/27f33fcbfcec4b42b6837807b7a0883f.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0627/16/EIML2HJO000181RV.html">被毒虫男友拖下水的女大学生</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0626/13/EIJPJMCH000181RV.html">领导，求你让我加班吧</a></li>
    </ul>
    </div>
    </li>
    <!-- 人间 结束 -->
    <!-- 大国小民 开始 -->
    <li class="cell cell_dgxm">
    <p class="tag_line">
    <span class="tags tag_dgxm">大国小民</span>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0624/14/EIEOBNCB000181RK.html" ne-role="detail">
    <h3>
                                    当不了官发不了财的读书人
                                </h3>
    <div class="photo">
    <img alt="当不了官发不了财的读书人" height="90" src="https://cms-bucket.ws.126.net/2019/06/24/b77e119ffeca477fa4bd2144b1fcb86c.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0620/16/EI4JRNO7000181RK.html">四个博士，一地鸡毛</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0618/12/EHV0QRVG000181RK.html">医闹得逞后，伤害的到底是谁</a></li>
    </ul>
    </div>
    </li>
    <!-- 大国小民 结束 -->
    <!-- 三三有梗 开始 -->
    <li class="cell cell_dada">
    <p class="tag_line">
    <span class="tags tag_dada">三三有梗</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0627/11/EIM57O490001885B.html" ne-role="detail">
    <h3>
                                    据说99%的人在图书馆一定会碰上......
                                </h3>
    <div class="photo">
    <img alt="据说99%的人在图书馆一定会碰上......" height="90" src="https://cms-bucket.ws.126.net/2019/06/27/06eb8f4a3d4647bf9360ff5e71f003b8.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0626/15/EIK0IJT40001885B.html">我可能，得了种，前任病</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0617/09/EHS57H4L0001885B.html">那些KO不掉我的,最终成了我的OK</a></li>
    </ul>
    </div>
    </li>
    <!-- 三三有梗 结束 -->
    <!-- 三三映画 开始 -->
    <!-- 三三映画 结束 -->
    <!-- 我去1990 开始 -->
    <li class="cell cell_wq1990">
    <p class="tag_line">
    <span class="tags tag_wq1990">我去1990</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/11/EIOL94760001885B.html" ne-role="detail">
    <h3>
                                    直男幼稚行为大赏
                                </h3>
    <div class="photo">
    <img alt="直男幼稚行为大赏" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/0b3890cd2f4b473fa0127b5e33ae6ccf.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0624/12/EIEFGMVL0001885B.html">打个赌，爱情友情你分不清楚</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0621/12/EI6NKDTU0001885B.html">不会唱歌的人进 KTV 以后有多惨</a></li>
    </ul>
    </div>
    </li>
    <!-- 我去1990 结束 -->
    <!-- 轻松一刻 开始 -->
    <li class="cell cell_qsyk">
    <p class="tag_line">
    <span class="tags tag_qsyk">轻松一刻</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/19/EIPIQT4O000181BR.html" ne-role="detail">
    <h3>
                                    彩票一直都不中，我却忍不住要买
                                </h3>
    <div class="photo">
    <img alt="彩票一直都不中，我却忍不住要买" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f44265c5b4ef4a11a99eedbde7c49833.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0627/17/EIMPGJAU000181BR.html">原来"神仙眷侣"离婚,也是一地鸡毛</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0626/18/EIK95RV0000181BR.html">我宣布，北大清华这对CP锁死了！</a></li>
    </ul>
    </div>
    </li>
    <!-- 轻松一刻 结束 -->
    <!-- 槽值 开始 -->
    <li class="cell cell_caozhi">
    <p class="tag_line">
    <span class="tags tag_caozhi">槽值</span>
    </p>
    <div class="column_main">
    <a class="detail" href="http://caozhi.news.163.com/19/0623/22/EID0CBIH000181TI.html" ne-role="detail">
    <h3>
                                    佟丽娅，这次你赢了
                                </h3>
    <div class="photo">
    <img alt="佟丽娅，这次你赢了" height="90" src="https://cms-bucket.ws.126.net/2019/06/23/67d24242d479451ea705e26296187f78.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://caozhi.news.163.com/19/0623/15/EIC9LGSP000181TI.html">千万别在深夜点开这神作</a></li>
    <li class="twoli"><a href="http://caozhi.news.163.com/19/0618/19/EHVRID7G000181TI.html">那个发“嗯”的人，已被踢出群聊</a></li>
    </ul>
    </div>
    </li>
    <!-- 槽值 结束 -->
    <!-- 谈心社 开始 -->
    <li class="cell cell_tanxinshe">
    <p class="tag_line">
    <span class="tags tag_tanxinshe">谈心社</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/17/EIPCOKEA0001982T.html" ne-role="detail">
    <h3>
                                    王宝强母亲去世：来日方长是人生的错觉
                                </h3>
    <div class="photo">
    <img alt="王宝强母亲去世：来日方长是人生的错觉" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/ecd0de8b8dc0402da72d814bde76f06e.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0627/13/EIMC0EDH0001982T.html">宋仲基宋慧乔离婚：再美的爱情也会过期</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0626/17/EIK6AD550001982T.html">杨紫冰箱藏药，戳穿最怂瞬间</a></li>
    </ul>
    </div>
    </li>
    <!-- 谈心社 结束 -->
    <!-- 看客 开始 -->
    <li class="cell cell_kanke">
    <p class="tag_line">
    <a class="tags tag_kanke" href="http://renjian.163.com/special/renjian_kanke/">看客</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0628/11/EIOMK185000199ET.html" ne-role="detail">
    <h3>
                                    我奶茶都戒了，日本人才知道它的好
                                </h3>
    <div class="photo">
    <img alt="我奶茶都戒了，日本人才知道它的好" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f35eceb8d111496693e8f77a71a49cba.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0620/11/EI43PM8Q000199ET.html">美国堕胎残酷物语</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0613/11/EHI39FML000199ET.html">跑腿小哥提供的十万种服务</a></li>
    </ul>
    </div>
    </li>
    <!-- 看客 结束 -->
    <!-- 身体密码 开始 -->
    <li class="cell cell_stpwd">
    <p class="tag_line">
    <a class="tags tag_stpwd" href="http://jiankang.163.com/special/zhutierji/?type=3">身体密码</a>
    </p>
    <div class="column_main">
    <a class="detail" href="https://jiankang.163.com/19/0625/11/EIH061CM0038804G.html" ne-role="detail">
    <h3>
                                    防晒，99%的人都做错了……
                                </h3>
    <div class="photo">
    <img alt="防晒，99%的人都做错了……" height="90" src="https://cms-bucket.ws.126.net/2019/06/25/f260b6843fca4702bb5e4e316600f113.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://jiankang.163.com/19/0617/14/EHSN7PPV0038804G.html">当代人减肥：迈不过25岁这道坎</a></li>
    <li class="twoli"><a href="https://jiankang.163.com/19/0608/15/EH5J9IGA00388AD5.html">多年后 无数中年人仍会被高考吓醒</a></li>
    </ul>
    </div>
    </li>
    <!-- 身体密码 结束 -->
    <!-- 哒哒 开始 -->
    <!-- 哒哒 结束 -->
    </ul>
    </div>
    <div id="js_baseline"></div>
    <span class="white_bg" id="js_white_bg"></span>
    </div>
    </div>
    </div>
    </div>
    <!-- 原创栏目 结束 -->
    <!-- 中间新闻 开始 -->
    <div class="main_center_news">
    <!-- 头条新闻 -->
    <div class="mod_top_news2" id="js_top_news">
    <h2>
    <a href="https://news.163.com/19/0628/16/EIP8R4SV000189FH.html">央视独家：习近平会见日本首相</a>
    </h2>
    <ul class="top_news_ul">
    <li><a href="https://news.163.com/19/0628/16/EIP8N52U0001875N.html">外交部回应中美元首会面</a>|<a href="https://news.163.com/19/0628/14/EIOVIP2500018AP1.html" target="_blank">特朗普会见普京 笑称:不要干预美国大选哦</a></li>
    <li><a href="https://news.163.com/19/0628/16/EIP7KOH70001875P.html">住建部:加快垃圾分类处理设施建设</a>|<a href="https://news.163.com/19/0628/16/EIP8F9QQ0001875P.html" target="_blank">袁仁国被公诉:受贿数额特别巨大</a></li>
    <li><a href="https://news.163.com/19/0628/13/EIOSPGLJ0001899O.html">湖南耒阳人大常委会原主任携子主动投案</a>|<a href="https://news.163.com/19/0628/13/EIOUHOB70001875P.html" target="_blank">美的48小时内被骗10亿资金</a></li>
    </ul>
    <h2 class="top_news_title">
    <a href="https://news.163.com/19/0628/19/EIPH3F1V0001875P.html">垃圾分类逼疯上海人？别笑！马上轮到这46个城市</a>
    </h2>
    <ul class="top_news_ul">
    <li><a href="https://news.163.com/19/0628/19/EIPILCJ70001875P.html">女子酒后澡堂一打六被刑拘</a>|<a href="https://news.163.com/19/0628/18/EIPFI0KN0001875P.html" target="_blank">杀人案嫌犯向警察开枪拒捕 被当场击毙</a></li>
    <li><a href="https://news.163.com/19/0628/16/EIP8RHM70001875P.html">95后飙摩托车追高铁发抖音被刑拘</a>|<a href="https://news.163.com/19/0628/16/EIP7B7RP0001899O.html" target="_blank">母亲担心儿子粗心在其手背"刺"字</a></li>
    <li><a href="https://news.163.com/19/0628/15/EIP4Q6BQ0001899O.html">女子高铁上劝老人看好小孩被骂</a>|<a href="https://news.163.com/19/0628/16/EIP8QO5Q0001875P.html" target="_blank">南京杀妻案死者姑妈：侄女生前要强</a></li>
    </ul>
    </div>
    <!-- 广告 开始 -->
    <div class="mod_top_news_ad">
    <!-- 16新闻首页01小通栏 -->
    <a class="ad_hover_href" href="http://gb.corp.163.com/gb/legal.html"></a>
    <iframe border="0" frameborder="no" height="50" marginheight="0" marginwidth="0" scrolling="no" src="https://g.163.com/r?site=netease&amp;affiliate=news&amp;cat=homepage&amp;type=logo600x50&amp;location=1" width="600"></iframe>
    </div>
    <!-- 广告 结束 -->
    <!-- 特别报道 开始 -->
    <div class="mod_important_news none">
    <h5><label>特别报道</label></h5>
    <h2>
    <a href="http://news.163.com/16/0721/19/BSH7V8QF00014JB6.html">辽宁遭暴雨侵袭致城市内涝 紧急转移12万人</a>
    </h2>
    <ul class="top_news_ul">
    <li><a href="http://news.163.com/16/0721/10/BSG7HOH20001124J.html">民政部:北方暴雨75人死亡失踪</a>|<a href="http://news.163.com/16/0721/12/BSGG5VK300011229.html" target="_blank">北京发生山洪灾害 铲车翻倒4人被困</a></li>
    <li><a href="http://news.163.com/16/0721/12/BSGHHVLK00011229.html">搜救犬水灾救援22天殉职 主人:它太累了</a>|<a href="http://news.163.com/16/0721/07/BSFUFFP800014AED.html" target="_blank">姐妹被洪水卷走警方拒立案</a></li>
    </ul>
    <div class="mod_important_pic">
    <ul class="clearfix">
    <li>
    <a href="http://news.163.com/photoview/00AN0001/2189402.html?from=ph_ss#p=BSG716GE00AN0001">
    <img height="120" src="http://img3.cache.netease.com/news/2016/7/21/20160721131401d35e2.jpg" width="190"/>
    <span class="bg"></span>
    <h3>河南遇强降雨 9.8万人转移</h3>
    </a>
    </li>
    <li>
    <a href="http://news.163.com/photoview/00AP0001/2189377.html?from=ph_ss#p=BSFTQ99H00AP0001">
    <img height="120" src="http://img3.cache.netease.com/news/2016/7/21/201607211319466e84e.jpg" width="190"/>
    <span class="bg"></span>
    <h3>女主播直播暴雨 浑身湿透</h3>
    </a>
    </li>
    <li>
    <a href="http://news.163.com/photoview/00AP0001/2189389.html?from=ph_ss#p=BSG1S9AM00AP0001">
    <img height="120" src="http://img5.cache.netease.com/news/2016/7/21/20160721132119ef59b.jpg" width="190"/>
    <span class="bg"></span>
    <h3>湖北民众省道上趟水摸鱼</h3>
    </a>
    </li>
    </ul>
    </div>
    </div>
    <!-- 特别报道 结束 -->
    <!-- 网易公开课 开始-->
    <div class="mod_netes_origina" ne-module="/news/index2016_rmd/modules/slide/slide.js">
    <script _keep="true" type="text/javascript">
        window.GGKSLIDEDATA = [
                                                                             {
                "title":"你多久没读完一本书了？带你克服读书拖延症",
                "imgsrc":"https://cms-bucket.ws.126.net/2019/06/26/225c40fe7f9141a8852f70d20c381f8b.jpeg?imageView&thumbnail=600y250",
                "link":"https://vip.open.163.com/courses/2531?p=xs_zt04"
            }
                                                             ,
                    {
                "title":"曾国藩：普通人怎样通过自我努力改写命运？",
                "imgsrc":"https://cms-bucket.ws.126.net/2019/05/16/b0ba21dfb7ef4716a1275a2c1914832a.jpeg?imageView&thumbnail=600y250",
                "link":"https://vip.open.163.com/courses/1047?p=xs_zt03"
            }
                                                             ,
                    {
                "title":"你单一的收入模式，拖垮的是你财富积累速度",
                "imgsrc":"https://cms-bucket.ws.126.net/2019/03/21/fe5cf147142b414793a6326f654b41ce.jpeg?imageView&thumbnail=600y250",
                "link":"https://vip.open.163.com/courses/3547?p=xs_zt04"
            }
                                                             ,
                    {
                "title":"健身VS不健身，完全是两种不同的人生",
                "imgsrc":"https://cms-bucket.nosdn.127.net/2018/11/12/94fbcf460348460f9b73300aa1948cb3.jpeg?imageView&thumbnail=600y250",
                "link":"https://vip.open.163.com/courses/192?p=xs_zt02"
            }
                ];
    </script>
    <div class="mod_idx_focus" ne-module="/modules/slide/slide.js" ne-props="events:mouseover;interval:4000;topicid=000501EP;listnum=8;pointstart=80;pointend=100;" ne-state="slideMethod:left;events=mouseover;interval=4000">
    <div class="hd">
    <h2><a href="https://open.163.com/">网易公开课</a></h2>
    <div class="focus_ctrl">
    <span ne-role="slide-nav"></span>
    <span ne-role="slide-nav"></span>
    <span ne-role="slide-nav"></span>
    <span ne-role="slide-nav"></span>
    </div>
    </div>
    <a class="focus_prev" ne-role="slide-prev"></a>
    <a class="focus_next" ne-role="slide-next"></a>
    <div class="focus_body" ne-role="slide-body">
    <ul ne-role="slide-scroll">
    <script ne-foreach="gkkdatalist" type="text/template">
                <li <%if(__i == 0){%>class="current"<%}%> ne-role="slide-page">
                    <a href="<%=link%>" title="<%=title%>" class="photo"><img src="<%=imgsrc%>" width="600" height="250" alt="<%=title%>"/></a>
                    <span class="bg"></span>
                    <h3>
                        <a href="<%=link%>"><%=title%></a>
                    </h3>
                </li>
                </script>
    </ul>
    <span class="ad_hover_pic">广告</span>
    </div>
    </div>
    </div>
    <!-- 网易公开课 结束-->
    <!-- 信息流 开始-->
    <div class="mod_datalist" ne-extend="/news/index2016_rmd/modules/datalist2016/config.js" ne-module="/news/index2016_rmd/modules/datalist2016/datalist2016.js">
    <div class="newsdata_wrap" ne-module="/modules/tabs/tabs.js" ne-on="showed:changepanel" ne-state="showhide:true;delay:400;">
    <div class="newsdata_nav" ne-class="{{myState.fixedTop ? 'fixed_top':''}}">
    <ul class="clearfix">
    <li class="nav_item">
    <a class="nav_name no_cursor" href="javascript:;" ne-role="tab-nav" target="_self">
                        要闻
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name no_cursor" href="{{myState.channelbendiurl}}" ne-class="{{myState.bendiTstyle ? 'bendistyle' : ''}}" ne-role="tab-nav" target="{{myState.channelbendiurl == 'javascript:;' ? '_self' : '_blank'}}">
    <strong ne-text="{{myState.bendiCity}}"></strong>
    <span class="nav_item_ink"></span>
    </a>
    </li>
    <!-- <li class="nav_item">
                    <a class="nav_name" ne-role="tab-nav" href="http://news.163.com/shehui/">
                        社会
                        <span class="nav_item_ink"></span>
                    </a>
                </li> -->
    <li class="nav_item">
    <a class="nav_name" href="http://news.163.com/domestic/" ne-role="tab-nav">
                        国内
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name" href="http://news.163.com/world/" ne-role="tab-nav">
                        国际
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name no_cursor" href="javascript:;" ne-role="tab-nav" target="_self">
                        独家
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name" href="http://war.163.com/" ne-role="tab-nav">
                        军事
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name" href="http://money.163.com/" ne-role="tab-nav">
                        财经
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    <li class="nav_item">
    <a class="nav_name" href="http://tech.163.com/" ne-role="tab-nav">
                        科技
                        <span class="nav_item_ink"></span>
    </a>
    </li>
    </ul>
    <a class="more" href="javascript:;" ne-class="{{myState.morechannel ? 'more_hover': ''}}" ne-mouseout="morehideChannel()" ne-mouseover="moreShowChannel()" ne-role="morebtn" target="_self">更多</a>
    <div class="more_list" ne-click="moreList($event)" ne-role="more_list" ne-show="{{myState.morechannel}}">
    <!-- <a ne-role="tab-nav" href="http://tech.163.com/">科技</a> -->
    <a href="http://sports.163.com/" ne-role="tab-nav">体育</a>
    <a href="http://ent.163.com/" ne-role="tab-nav">娱乐</a>
    <a href="http://lady.163.com/" ne-role="tab-nav">时尚</a>
    <a href="http://auto.163.com/" ne-role="tab-nav">汽车</a>
    <a href="{{myState.channelhouseurl}}" ne-role="tab-nav">房产</a>
    <a href="http://news.163.com/air/" ne-role="tab-nav">航空</a>
    <a href="http://jiankang.163.com/" ne-role="tab-nav">健康</a>
    </div>
    </div>
    <a class="newsdata_prev" href="#prev" ne-class="{{myState.fixedTop ? 'fixed_data_show': ''}}" ne-click="tabPrevFn($event);" ne-hide="{{myState.iPad}}">
    <span></span>
    <div class="newsdata_btn_name">{{myState.preBtnName}}</div>
    </a>
    <a class="newsdata_next" href="#next" ne-class="{{myState.fixedTop ? 'fixed_data_show': ''}}" ne-click="tabNextFn($event);" ne-hide="{{myState.iPad}}">
    <span></span>
    <div class="newsdata_btn_name">{{myState.nextBtnName}}</div>
    </a>
    <ul class="newsdata_list" ne-class="{{myState.fixedTop ? 'fixed_bar_padding': ''}} {{myState.bgLoading ? 'bgloading': 'noloading'}}">
    <li class="newsdata_item" ne-repeat="body in navList" ne-role="tab-body">
    <div class="ndi_main" ne-class="{{myState.message &gt; 0 ? 'show_message':''}}">
    <script ne-repeat="newrow in datalist[__i]" type="text/template">
                    <%if(newrow.style == "iframe"){%>
                        <div class="at_item info_ad_item news_iframe_ad" adType="infoAd" ne-click="adClickTracker(<%=newrow.infoAdIdx%>,'infoAd')">
                            <iframe src="<%=newrow.iframe[0].link%>" width="<%=newrow.iframe[0].iframewidth || 600 %>" height="<%=newrow.iframe[0].iframeheight || 100 %>" frameborder="0" border="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
                        </div>
                    <%}else if(newrow.style == "docAD"){%>
                        <div class="at_item info_ad_item news_article clearfix" adType="infoAd" ne-click="adClickTracker(<%=newrow.infoAdIdx%>,'infoAd')">
                            <a href="<%=newrow.relatedActionLinks[0].url%>" class="na_pic">
                                <img src="<%=newrow.resources[0].urls[0]%>" width="140" height="88">
                            </a>
                            <div class="na_detail clearfix">
                                <div class="news_title">
                                    <h3><strong><a href="<%=newrow.relatedActionLinks[0].url%>"><%=newrow.title%></a>
                                    </strong></h3>
                                </div>
                            </div>
                            <div class="ad_detail clearfix">
                                <span class="tg_tag"><%=newrow.source%></span>
                                <span class="keywords" ne-html="<%=newrow.content%>"></span>
                            </div>
                        </div>
                    <%} else if(newrow.style == "photosetAD"){%>
                        <div class="at_item info_ad_item news_photoview clearfix news_ad_photoview" adType="infoAd" ne-click="adClickTracker(<%=newrow.infoAdIdx%>,'infoAd')">
                            <div class="news_title">
                                <h3><strong><a href="<%=newrow.relatedActionLinks[0].url%>"><%=newrow.title%></a></strong></h3>
                            </div>
                            <div class="np_pic">
                                <a href="<%=newrow.relatedActionLinks[0].url%>">
                                    <span class="p_img3">
                                        <img src="<%=newrow.resources[0].urls[0]%>" width="190" height="120">
                                    </span>
                                    <span class="p_img3">
                                        <img src="<%=newrow.resources[0].urls[1]%>" width="190" height="120">
                                    </span>
                                    <span class="p_img3">
                                        <img src="<%=newrow.resources[0].urls[2]%>" width="190" height="120" class="pic_last">
                                    </span>
                                </a>
                            </div>
                            <div class="ad_detail clearfix">
                                <span class="tg_tag"><%=newrow.source%></span>
                                <span class="keywords" ne-html="<%=newrow.content%>"></span>
                            </div>
                        </div>
                    <%} else if(newrow.style == "columsAD"){%>
                        <div class="at_item info_ad_item news_special clearfix news_ad_special" adType="infoAd" ne-click="adClickTracker(<%=newrow.infoAdIdx%>,'infoAd')">
                            <div class="news_title">
                                <h3><strong><a href="<%=newrow.relatedActionLinks[0].url%>"><%=newrow.title%></a></strong></h3>
                            </div>
                            <a href="<%=newrow.relatedActionLinks[0].url%>" class="ns_pic"><img src="<%=newrow.resources[0].urls[0]%>" width="600" height="200"></a>
                            <div class="ad_detail clearfix">
                                <span class="tg_tag"><%=newrow.source%></span>
                                <span class="keywords" ne-html="<%=newrow.content%>"></span>
                            </div>
                        </div>
                    <%} else if(newrow.imgurl && newrow.add1 && newrow.add2 && /\.jpg$|\.png$|\.jpeg$|\.gif$/.test(newrow.imgurl) && /\.jpg$|\.png$|\.jpeg$|\.gif$/.test(newrow.add1) && /\.jpg$|\.png$|\.jpeg$|\.gif$/.test(newrow.add2)){%>
                        <div class="data_row news_photoview clearfix <%if(__i == 0){%>news_first <%}%>">
                            <div class="news_title">
                                <h3><a href="<%=newrow.docurl%>"><%=newrow.title%></a></h3>
                            </div>
                            <div class="np_pic">
                                <a href="<%=newrow.docurl%>">
                                    <span class="p_img3">
                                    <%if(newrow.imgurl.indexOf('gif') != -1){%>
                                    <img src="<%=newrow.imgurl%>" width="190" height="120" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%} else {%> 
                                    <img src="<%=newrow.imgurl%>?imageView&thumbnail=190y120&quality=85" width="190" height="120" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%}%> 
                                    </span>
                                    <span class="p_img3">
                                    <%if(newrow.add1.indexOf('gif') != -1){%>
                                    <img src="<%=newrow.add1%>" width="190" height="120" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%} else {%> 
                                    <img src="<%=newrow.add1%>?imageView&thumbnail=190y120&quality=85" width="190" height="120" onerror="javascript:this.src='https://static.ws.126.net/f2e/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%}%> 
                                    </span>
                                    <span class="p_img3">
                                    <%if(newrow.add2.indexOf('gif') != -1){%>
                                    <img src="<%=newrow.add2%>" width="190" height="120" class="pic_last" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%} else {%> 
                                    <img src="<%=newrow.add2%>?imageView&thumbnail=190y120&quality=85" width="190" height="120" class="pic_last" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                    <%}%> 
                                    </span>
                                </a>
                            </div>
                            <div class="np_detail clearfix">
                                <div class="news_tag">
                                    <%if(newrow.channelname && newrow.channelname != "shehui" && newrow.channelname != "guonei" && newrow.channelname != "guoji" && newrow.channelname != "dada" && newrow.channelname != "war" && newrow.channelname != "hangkong"){%>
                                        <%if(newrow.tlastid != ""){%>
                                            <strong class="barlink"><%=newrow.tlastid%></strong>
                                        <%}else if(newrow.label != ""){%>
                                            <a href="<%=newrow.tlink%>" class="link link_more">
                                            <em><%=newrow.label%></em></a>
                                        <%}%> 
                                    <%}%>
                                    <%if(newrow.keywords.length > 0){%>
                                        <div class="keywords">
                                        <%bowlder.each(newrow.keywords,function(k){%>
                                            <a href="<%=k.akey_link%>"><%=k.keyname%></a>
                                        <%})%> 
                                        </div>
                                    <%}%> 
                                    <%if(newrow.time){%>
                                        <span class="time"><%=formatTime(newrow.time)%></span>
                                    <%}%> 
                                </div>
                                <div class="share-join clearfix">
                                    <%if(newrow.tienum != ""){%>
                                    <a class="post_recommend_tie right" href="<%=newrow.commenturl%>" >
                                        <div class="post_recommend_tie_wrap">
                                            <span class="post_recommend_tie_icon icons"><%=newrow.tienum%></span> 
                                            <span class="post_recommend_tie_text"><i>跟贴</i><%=newrow.tienum%></span>
                                        </div>
                                    </a>
                                    <%}%>
                                    <div class="ne-shares-parent right">
                                        <span href="#share" title="分享" class="ne-shares-arr"></span>
                                        <div class="share-join-item" ne-module="/modules/shares/shares.js" ne-state="cls.hover:ne-shares-open;title:<%=newrow.title%>;url:<%=newrow.docurl%>;pic:<%=newrow.imgurl%>" >
    <div class="ne-shares-pop6x1wrap" ne-role="share-wrap">
    <ul class="ne-shares-pop6x1">
        <li>
            <a ne-click="share('yixin')" href="http://yixin.im/#f=www">
                <span class="inner">
                    <i class="ep-share-icon ep-share-yixin"></i>
                    <span class="ep-share-name">易信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-mouseover="initWeixin()" href="javascript:" target="_self" class="ne-shares-weixin">
                <span class="inner">
                    <i class="ep-share-icon ep-share-weixin"></i>
                    <span class="ep-share-name">微信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-click="share('sina')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-sina"></i>
                    <span class="ep-share-name">微博</span>
                </span>
            </a>
        </li>
        <li class="last">
            <a ne-click="share('qzone')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-qzone"></i>
                    <span class="ep-share-name">QQ空间</span>
                </span>
            </a>
        </li>
    </ul>
    </div>
    <div class="ne-shares-qrwrap">
      <div class="ne-shares-qrarr"></div>
      <div ne-role="qrcode" class="ne-shares-qrcode"></div>
      <p>用微信扫码二维码</p><p>分享至好友和朋友圈</p>
    </div>
    </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    <%} else if(newrow.add1 && /\.jpg$|\.png$|\.jpeg$|\.gif$/.test(newrow.add1)){%>
                        <div class="data_row news_special clearfix <%if(__i == 0){%>news_first <%}%>">
                            <div class="news_title">
                                <h3><a href="<%=newrow.docurl%>"><%=newrow.title%></a></h3>
                                <%if(newrow.channelname && newrow.channelname != "shehui" && newrow.channelname != "guonei" && newrow.channelname != "guoji" && newrow.channelname != "dada" && newrow.channelname != "war" && newrow.channelname != "hangkong"){%>
                                    <%if(newrow.tlastid != ""){%>
                                        <strong class="barlink"><%=newrow.tlastid%></strong>
                                    <%}else if(newrow.label != ""){%>
                                        <a href="<%=newrow.tlink%>" class="link link_more">
                                        <em><%=newrow.label%></em></a>
                                    <%}%> 
                                <%}%>
                            </div>
                            <a href="<%=newrow.docurl%>" class="ns_pic">
                                <%if(newrow.add1.indexOf('gif') != -1){%>
                                <img src="<%=newrow.add1%>" alt="<%=newrow.title%>" width="600" height="300" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/special_error0106.jpg';">
                                <%} else {%> 
                                <img src="<%=newrow.add1%>?imageView&thumbnail=600y300&quality=85" alt="<%=newrow.title%>" width="600" height="300" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/special_error0106.jpg';">
                                <%}%> 
                            </a>
                        </div>
                    <%} else if(newrow.imgurl && newrow.imgurl != ""){%>
                        <div class="data_row news_article clearfix <%if(__i == 0){%>news_first<%}%>">
                            <%if(newrow.imgurl != ""){%>
                                <a href="<%=newrow.docurl%>" class="na_pic">
                                    <%if(newrow.imgurl.indexOf('gif') != -1){%>
                                    <img src="<%=newrow.imgurl%>" alt="<%=newrow.title%>" width="140" height="88" onerror="imgError(this)">
                                    <%} else {%> 
                                    <img src="<%=newrow.imgurl%>?imageView&thumbnail=140y88&quality=85" alt="<%=newrow.title%>" width="140" height="88" onerror="imgError(this)">
                                    <%}%> 
                                </a>
                            <%}%> 
                            <div class="na_detail clearfix <%if(newrow.imgurl == ""){%>no_pic<%}%>">
                                <div class="news_title">
                                    <h3><a href="<%=newrow.docurl%>"><%=newrow.title%></a></h3>
                                </div>
                                <div class="news_tag">
                                    <%if(newrow.channelname && newrow.channelname != "shehui" && newrow.channelname != "guonei" && newrow.channelname != "guoji" && newrow.channelname != "dada" && newrow.channelname != "war" && newrow.channelname != "hangkong"){%>
                                        <%if(newrow.tlastid != ""){%>
                                            <strong class="barlink"><%=newrow.tlastid%></strong>
                                        <%}else if(newrow.label != ""){%>
                                            <a href="<%=newrow.tlink%>" class="link link_more">
                                            <em><%=newrow.label%></em></a>
                                        <%}%> 
                                    <%}%>
                                    <%if(newrow.keywords && newrow.keywords.length > 0){%>
                                        <div class="keywords">
                                        <%bowlder.each(newrow.keywords,function(k){%>
                                            <a href="<%=k.akey_link%>"><%=k.keyname%></a>
                                        <%})%> 
                                        </div>
                                    <%}%> 
                                    <%if(newrow.time){%>
                                        <span class="time"><%=formatTime(newrow.time)%></span>
                                    <%}%> 
                                </div>
                                <div class="share-join clearfix">
                                    <a class="post_recommend_tie right" href="<%=newrow.commenturl%>" >
                                        <div class="post_recommend_tie_wrap">
                                            <span class="post_recommend_tie_icon icons"><%=newrow.tienum ? newrow.tienum : 0%></span> 
                                            <span class="post_recommend_tie_text"><i>跟贴</i><%=newrow.tienum%></span>
                                        </div>
                                    </a>
                                    <div class="ne-shares-parent right">
                                        <span href="#share" title="分享" class="ne-shares-arr"></span>
                                        <div class="share-join-item" ne-module="/modules/shares/shares.js" ne-state="cls.hover:ne-shares-open;title:<%=newrow.title%>;url:<%=newrow.docurl%>;pic:<%=newrow.imgurl%>" >
    <div class="ne-shares-pop6x1wrap" ne-role="share-wrap">
    <ul class="ne-shares-pop6x1">
        <li>
            <a ne-click="share('yixin')" href="http://yixin.im/#f=www">
                <span class="inner">
                    <i class="ep-share-icon ep-share-yixin"></i>
                    <span class="ep-share-name">易信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-mouseover="initWeixin()" href="javascript:" target="_self" class="ne-shares-weixin">
                <span class="inner">
                    <i class="ep-share-icon ep-share-weixin"></i>
                    <span class="ep-share-name">微信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-click="share('sina')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-sina"></i>
                    <span class="ep-share-name">微博</span>
                </span>
            </a>
        </li>
        <li class="last">
            <a ne-click="share('qzone')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-qzone"></i>
                    <span class="ep-share-name">QQ空间</span>
                </span>
            </a>
        </li>
    </ul>
    </div>
    <div class="ne-shares-qrwrap">
      <div class="ne-shares-qrarr"></div>
      <div ne-role="qrcode" class="ne-shares-qrcode"></div>
      <p>用微信扫码二维码</p><p>分享至好友和朋友圈</p>
    </div>
    </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    <%} else if(newrow.pics3 && newrow.pics3.length >= 3){%>
                        <div class="data_row news_photoview clearfix <%if(__i == 0){%>news_first <%}%>">
                            <div class="news_title">
                                <h3><a href="<%=newrow.docurl%>"><%=newrow.title%></a></h3>
                            </div>
                            <div class="np_pic">
                                <a href="<%=newrow.docurl%>">
                                    <%bowlder.each(newrow.pics3,function(n){%>
                                        <span class="p_img3">
                                        <img src="<%=n.pic%>" width="190" height="120" onerror="javascript:this.src='https://static.ws.126.net/f2e/news/index2016_rmd/images/pic3_error0106.jpg';">
                                        </span>
                                    <%})%> 
                                </a>
                            </div>
                            <div class="np_detail clearfix">
                                <div class="news_tag">
                                    <%if(newrow.channelname && newrow.channelname != "shehui" && newrow.channelname != "guonei" && newrow.channelname != "guoji" && newrow.channelname != "dada" && newrow.channelname != "war" && newrow.channelname != "hangkong"){%>
                                        <%if(newrow.tlastid != ""){%>
                                            <strong class="barlink"><%=newrow.tlastid%></strong>
                                        <%}else if(newrow.label != ""){%>
                                            <a href="<%=newrow.tlink%>" class="link link_more">
                                            <em><%=newrow.label%></em></a>
                                        <%}%> 
                                    <%}%>
                                    <%if(newrow.keywords && newrow.keywords.length > 0){%>
                                        <div class="keywords">
                                        <%bowlder.each(newrow.keywords,function(k){%>
                                            <a href="<%=k.akey_link%>"><%=k.keyname%></a>
                                        <%})%> 
                                        </div>
                                    <%}%> 
                                    <%if(newrow.time){%>
                                        <span class="time"><%=formatTime(newrow.time)%></span>
                                    <%}%> 
                                </div>
                                <div class="share-join clearfix">
                                    <a class="post_recommend_tie right" href="<%=newrow.commenturl%>" >
                                        <div class="post_recommend_tie_wrap">
                                            <span class="post_recommend_tie_icon icons"><%=newrow.tienum%></span> 
                                            <span class="post_recommend_tie_text"><i>跟贴</i><%=newrow.tienum%></span>
                                        </div>
                                    </a>
                                    <div class="ne-shares-parent right">
                                        <span href="#share" title="分享" class="ne-shares-arr"></span>
                                        <div class="share-join-item" ne-module="/modules/shares/shares.js" ne-state="cls.hover:ne-shares-open;title:<%=newrow.title%>;url:<%=newrow.docurl%>;pic:<%=newrow.imgurl%>" >
    <div class="ne-shares-pop6x1wrap" ne-role="share-wrap">
    <ul class="ne-shares-pop6x1">
        <li>
            <a ne-click="share('yixin')" href="http://yixin.im/#f=www">
                <span class="inner">
                    <i class="ep-share-icon ep-share-yixin"></i>
                    <span class="ep-share-name">易信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-mouseover="initWeixin()" href="javascript:" target="_self" class="ne-shares-weixin">
                <span class="inner">
                    <i class="ep-share-icon ep-share-weixin"></i>
                    <span class="ep-share-name">微信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-click="share('sina')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-sina"></i>
                    <span class="ep-share-name">微博</span>
                </span>
            </a>
        </li>
        <li class="last">
            <a ne-click="share('qzone')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-qzone"></i>
                    <span class="ep-share-name">QQ空间</span>
                </span>
            </a>
        </li>
    </ul>
    </div>
    <div class="ne-shares-qrwrap">
      <div class="ne-shares-qrarr"></div>
      <div ne-role="qrcode" class="ne-shares-qrcode"></div>
      <p>用微信扫码二维码</p><p>分享至好友和朋友圈</p>
    </div>
    </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    <%} else {%>
                        <div class="data_row news_article clearfix <%if(__i == 0){%>news_first<%}%>" i={{__i}}>
                            <div class="na_detail clearfix no_pic">
                                <div class="news_title">
                                    <h3><a href="<%=newrow.docurl%>"><%=newrow.title%></a></h3>
                                </div>
                                <div class="news_tag">
                                    <%if(newrow.channelname && newrow.channelname != "shehui" && newrow.channelname != "guonei" && newrow.channelname != "guoji" && newrow.channelname != "dada" && newrow.channelname != "war" && newrow.channelname != "hangkong"){%>
                                        <%if(newrow.tlastid != ""){%>
                                            <strong class="barlink"><%=newrow.tlastid%></strong>
                                        <%}else if(newrow.label != ""){%>
                                            <a href="<%=newrow.tlink%>" class="link link_more">
                                            <em><%=newrow.label%></em></a>
                                        <%}%> 
                                    <%}%>
                                    <%if(newrow.keywords && newrow.keywords.length > 0){%>
                                        <div class="keywords">
                                        <%bowlder.each(newrow.keywords,function(k){%>
                                            <a href="<%=k.akey_link%>"><%=k.keyname%></a>
                                        <%})%> 
                                        </div>
                                    <%}%> 
                                    <%if(newrow.time){%>
                                        <span class="time"><%=formatTime(newrow.time)%></span>
                                    <%}%> 
                                </div>
                                <div class="share-join clearfix">
                                    <a class="post_recommend_tie right" href="<%=newrow.commenturl%>" >
                                        <div class="post_recommend_tie_wrap">
                                            <span class="post_recommend_tie_icon icons"><%=newrow.tienum ? newrow.tienum : 0%></span> 
                                            <span class="post_recommend_tie_text"><i>跟贴</i><%=newrow.tienum%></span>
                                        </div>
                                    </a>
                                    <div class="ne-shares-parent right">
                                        <span href="#share" title="分享" class="ne-shares-arr"></span>
                                        <div class="share-join-item" ne-module="/modules/shares/shares.js" ne-state="cls.hover:ne-shares-open;title:<%=newrow.title%>;url:<%=newrow.docurl%>;pic:<%=newrow.imgurl%>" >
    <div class="ne-shares-pop6x1wrap" ne-role="share-wrap">
    <ul class="ne-shares-pop6x1">
        <li>
            <a ne-click="share('yixin')" href="http://yixin.im/#f=www">
                <span class="inner">
                    <i class="ep-share-icon ep-share-yixin"></i>
                    <span class="ep-share-name">易信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-mouseover="initWeixin()" href="javascript:" target="_self" class="ne-shares-weixin">
                <span class="inner">
                    <i class="ep-share-icon ep-share-weixin"></i>
                    <span class="ep-share-name">微信</span>
                </span>
            </a>
        </li>
        <li>
            <a ne-click="share('sina')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-sina"></i>
                    <span class="ep-share-name">微博</span>
                </span>
            </a>
        </li>
        <li class="last">
            <a ne-click="share('qzone')" href="javascript:">
                <span class="inner">
                    <i class="ep-share-icon ep-share-qzone"></i>
                    <span class="ep-share-name">QQ空间</span>
                </span>
            </a>
        </li>
    </ul>
    </div>
    <div class="ne-shares-qrwrap">
      <div class="ne-shares-qrarr"></div>
      <div ne-role="qrcode" class="ne-shares-qrcode"></div>
      <p>用微信扫码二维码</p><p>分享至好友和朋友圈</p>
    </div>
    </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    <%}%>
                    </script>
    </div>
    </li>
    </ul>
    <div class="load_more_foot" id="load_more_foot"></div>
    <a class="load_more_btn" ne-click="clickLoadMore();" ne-hide="{{myState.counter &gt;= navList[myState.ndNavIndex].totalPage || myState.counter == 0}}" target="_self">
    <div class="post_addmore" ne-visible="{{myState.counter &lt; navList[myState.ndNavIndex].totalPage &amp;&amp; !myState.loading}}">
    <i>+</i>
    <span>加载更多</span>
    </div>
    <div class="post_adding" ne-show="{{myState.loading}}">
    <i>+</i>
    <span>加载中...</span>
    </div>
    </a>
    <div class="load_more_tip" ne-show="{{myState.counter &gt;= navList[myState.ndNavIndex].totalPage}}">:-)已经到最后啦~</div>
    </div>
    </div>
    <!-- 信息流 结束 -->
    </div>
    <!-- 中间新闻 结束 -->
    <!-- 右侧栏目 开始 -->
    <div class="main_right_channel">
    <!-- 广告 -->
    <!-- 300*30 -->
    <!-- 新闻首页焦点图上方L特殊标识广告 开始-->
    <!-- <div class="mod_newsr_ad1">
    <a href="http://g.163.com/a?CID=45744&Values=2901173312&Redirect=http://clickc.admaster.com.cn/c/a73960,b1279435,c369,i0,m101,8a1,8b2,h"><img class="block mb10" width="300" height="30" src="http://img1.126.net/channel11/024018300301009.jpg" alt="广告"></a>
    </div> -->
    <!--新闻首页焦点图上方L特殊标识广告 结束-->
    <!-- 焦点图 开始-->
    <div class="mod_right_focus">
    <div ne-module="">
    <div class="mod_focus" ne-module="/modules/slide/slide.js" ne-state="slideMethod:left;events=mouseover;interval=4000;loop=true;">
    <div class="f_body" ne-role="slide-body">
    <ul class="f_main clearfix" ne-role="slide-scroll">
    <li ne-role="slide-page">
    <a href="http://g.163.com/a?CID=68685&amp;Values=1366894002&amp;Redirect=http://clk.gentags.net/clk/iv-10648/st-31/cr-2/oi-1303641/or-7535/adv-158/pcon-0/https%253A%252F%252Fent.163.com%252F19%252F0625%252F16%252FEIHG8HLF000398QL.html">
    <img height="400" src="http://nimg.ws.126.net/?url=https://yt-adp.ws.126.net/channel21/037408_300400_axry_20190626.jpg&amp;thumbnail=300x2147483647&amp;quality=75&amp;type=jpg" width="300"/>
    <span class="bg"></span>
    <h3>三金西瓜霜独家冠名网易封面故事</h3>
    </a>
    </li>
    <li ne-role="slide-page">
    <a href="http://news.163.com/photoview/00AP0001/2302561.html">
    <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/e5b070c1f96349b0829da88b41105903.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
    <span class="bg"></span>
    <h3>浒苔绿潮开始在山东沿海登陆</h3>
    </a>
    </li>
    <li ne-role="slide-page">
    <a href="http://news.163.com/photoview/00AP0001/2302559.html">
    <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/2792654fe66f4985879a8cc30a89a6cc.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
    <span class="bg"></span>
    <h3>广西南宁抓获涉传人员286名</h3>
    </a>
    </li>
    <li ne-role="slide-page">
    <a href="http://news.163.com/photoview/00AO0001/2302560.html">
    <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/202e20527525474cac861ba7e56a2dde.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
    <span class="bg"></span>
    <h3>民主党初选辩论次日:拜登现身</h3>
    </a>
    </li>
    </ul>
    </div>
    <div class="f_title">
    <span class="current" ne-role="slide-nav">1</span>
    <span class="" ne-role="slide-nav">2</span>
    <span class="" ne-role="slide-nav">3</span>
    <span class="" ne-role="slide-nav">4</span>
    </div>
    <a class="f_prev" ne-role="slide-prev">&lt;</a>
    <a class="f_next" ne-role="slide-next">&gt;</a>
    </div>
    </div>
    </div>
    <!-- 焦点图 结束-->
    <!-- 广告 开始-->
    <div class="mod_ad_toutu channel_relative_2016">
    <ul class="clearfix">
    <li><a href="http://baoxian.163.com/activity/act1605/index.html?from=mhds1605">免费领取iPhone6s</a></li>
    <li><a href="http://mall.163.com/mobile/fill.jsp?from=wwwtext">手机费快充超低折扣</a></li>
    <li><a href="http://baoxian.163.com/car/activitylist.html?from=mhdstbl">免费送现金红包！</a></li>
    <li><a href="http://piao.163.com/movie/47080.html?from=newsword">镜中多奇境依旧爱丽丝</a></li>
    </ul>
    <span class="channel_ad_text_2016">广告</span>
    </div>
    <!-- 广告 结束-->
    <!-- 右侧960原创栏目 开始 -->
    <div class="origina_column_960" id="js_origina_column_960">
    <div ne-module="/news/index2016_rmd/modules/originacolumn/originacolumn.js">
    <div class="origina_column_warp">
    <h2>
    <span>新闻各有态度</span>
    </h2>
    <div class="scroll_bd" ne-role="scroll_bd">
    <div class="scroll_column_bd">
    <ul class="scroll_ul">
    <!-- 回声 开始 -->
    <!-- 回声 结束 -->
    <!-- 数读 开始 -->
    <li class="cell cell_sd cell_hover">
    <p class="tag_line">
    <a class="tags tag_sd" href="http://data.163.com/special/datablog/">数读</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://data.163.com/19/0626/14/EIJQJG9L000181IU.html" ne-role="detail">
    <h3>
                                    中国哪里的地铁最拥挤？
                                </h3>
    <div class="photo">
    <img alt="中国哪里的地铁最拥挤？" height="90" src="https://cms-bucket.ws.126.net/2019/06/26/30e8760df3044e29a18fac3514dd22b1.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://data.163.com/19/0625/11/EIH0CQEK00019GOE.html">娶一个潮汕老婆到底是什么体验</a></li>
    <li class="twoli"><a href="http://data.163.com/19/0621/17/EI7BLS3600019GOE.html">不瞒你说，成都早餐好吃到爆</a></li>
    </ul>
    </div>
    </li>
    <!-- 数读 结束 -->
    <!-- 人间 开始 -->
    <li class="cell cell_rj">
    <p class="tag_line">
    <a class="tags tag_rj" href="http://renjian.163.com/">人间</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0628/14/EIP21K41000181RV.html" ne-role="detail">
    <h3>
                                    小白作者的变现之路
                                </h3>
    <div class="photo">
    <img alt="小白作者的变现之路" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/27f33fcbfcec4b42b6837807b7a0883f.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0627/16/EIML2HJO000181RV.html">被毒虫男友拖下水的女大学生</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0626/13/EIJPJMCH000181RV.html">领导，求你让我加班吧</a></li>
    </ul>
    </div>
    </li>
    <!-- 人间 结束 -->
    <!-- 大国小民 开始 -->
    <li class="cell cell_dgxm">
    <p class="tag_line">
    <span class="tags tag_dgxm">大国小民</span>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0624/14/EIEOBNCB000181RK.html" ne-role="detail">
    <h3>
                                    当不了官发不了财的读书人
                                </h3>
    <div class="photo">
    <img alt="当不了官发不了财的读书人" height="90" src="https://cms-bucket.ws.126.net/2019/06/24/b77e119ffeca477fa4bd2144b1fcb86c.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0620/16/EI4JRNO7000181RK.html">四个博士，一地鸡毛</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0618/12/EHV0QRVG000181RK.html">医闹得逞后，伤害的到底是谁</a></li>
    </ul>
    </div>
    </li>
    <!-- 大国小民 结束 -->
    <!-- 三三有梗 开始 -->
    <li class="cell cell_dada">
    <p class="tag_line">
    <span class="tags tag_dada">三三有梗</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0627/11/EIM57O490001885B.html" ne-role="detail">
    <h3>
                                    据说99%的人在图书馆一定会碰上......
                                </h3>
    <div class="photo">
    <img alt="据说99%的人在图书馆一定会碰上......" height="90" src="https://cms-bucket.ws.126.net/2019/06/27/06eb8f4a3d4647bf9360ff5e71f003b8.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0626/15/EIK0IJT40001885B.html">我可能，得了种，前任病</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0617/09/EHS57H4L0001885B.html">那些KO不掉我的,最终成了我的OK</a></li>
    </ul>
    </div>
    </li>
    <!-- 三三有梗 结束 -->
    <!-- 三三映画 开始 -->
    <!-- 三三映画 结束 -->
    <!-- 我去1990 开始 -->
    <li class="cell cell_wq1990">
    <p class="tag_line">
    <span class="tags tag_wq1990">我去1990</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/11/EIOL94760001885B.html" ne-role="detail">
    <h3>
                                    直男幼稚行为大赏
                                </h3>
    <div class="photo">
    <img alt="直男幼稚行为大赏" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/0b3890cd2f4b473fa0127b5e33ae6ccf.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0624/12/EIEFGMVL0001885B.html">打个赌，爱情友情你分不清楚</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0621/12/EI6NKDTU0001885B.html">不会唱歌的人进 KTV 以后有多惨</a></li>
    </ul>
    </div>
    </li>
    <!-- 我去1990 结束 -->
    <!-- 轻松一刻 开始 -->
    <li class="cell cell_qsyk">
    <p class="tag_line">
    <span class="tags tag_qsyk">轻松一刻</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/19/EIPIQT4O000181BR.html" ne-role="detail">
    <h3>
                                    彩票一直都不中，我却忍不住要买
                                </h3>
    <div class="photo">
    <img alt="彩票一直都不中，我却忍不住要买" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f44265c5b4ef4a11a99eedbde7c49833.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0627/17/EIMPGJAU000181BR.html">原来"神仙眷侣"离婚,也是一地鸡毛</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0626/18/EIK95RV0000181BR.html">我宣布，北大清华这对CP锁死了！</a></li>
    </ul>
    </div>
    </li>
    <!-- 轻松一刻 结束 -->
    <!-- 槽值 开始 -->
    <li class="cell cell_caozhi">
    <p class="tag_line">
    <span class="tags tag_caozhi">槽值</span>
    </p>
    <div class="column_main">
    <a class="detail" href="http://caozhi.news.163.com/19/0623/22/EID0CBIH000181TI.html" ne-role="detail">
    <h3>
                                    佟丽娅，这次你赢了
                                </h3>
    <div class="photo">
    <img alt="佟丽娅，这次你赢了" height="90" src="https://cms-bucket.ws.126.net/2019/06/23/67d24242d479451ea705e26296187f78.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://caozhi.news.163.com/19/0623/15/EIC9LGSP000181TI.html">千万别在深夜点开这神作</a></li>
    <li class="twoli"><a href="http://caozhi.news.163.com/19/0618/19/EHVRID7G000181TI.html">那个发“嗯”的人，已被踢出群聊</a></li>
    </ul>
    </div>
    </li>
    <!-- 槽值 结束 -->
    <!-- 谈心社 开始 -->
    <li class="cell cell_tanxinshe">
    <p class="tag_line">
    <span class="tags tag_tanxinshe">谈心社</span>
    </p>
    <div class="column_main">
    <a class="detail" href="https://news.163.com/19/0628/17/EIPCOKEA0001982T.html" ne-role="detail">
    <h3>
                                    王宝强母亲去世：来日方长是人生的错觉
                                </h3>
    <div class="photo">
    <img alt="王宝强母亲去世：来日方长是人生的错觉" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/ecd0de8b8dc0402da72d814bde76f06e.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://news.163.com/19/0627/13/EIMC0EDH0001982T.html">宋仲基宋慧乔离婚：再美的爱情也会过期</a></li>
    <li class="twoli"><a href="https://news.163.com/19/0626/17/EIK6AD550001982T.html">杨紫冰箱藏药，戳穿最怂瞬间</a></li>
    </ul>
    </div>
    </li>
    <!-- 谈心社 结束 -->
    <!-- 看客 开始 -->
    <li class="cell cell_kanke">
    <p class="tag_line">
    <a class="tags tag_kanke" href="http://renjian.163.com/special/renjian_kanke/">看客</a>
    </p>
    <div class="column_main">
    <a class="detail" href="http://renjian.163.com/19/0628/11/EIOMK185000199ET.html" ne-role="detail">
    <h3>
                                    我奶茶都戒了，日本人才知道它的好
                                </h3>
    <div class="photo">
    <img alt="我奶茶都戒了，日本人才知道它的好" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f35eceb8d111496693e8f77a71a49cba.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="http://renjian.163.com/19/0620/11/EI43PM8Q000199ET.html">美国堕胎残酷物语</a></li>
    <li class="twoli"><a href="http://renjian.163.com/19/0613/11/EHI39FML000199ET.html">跑腿小哥提供的十万种服务</a></li>
    </ul>
    </div>
    </li>
    <!-- 看客 结束 -->
    <!-- 身体密码 开始 -->
    <li class="cell cell_stpwd">
    <p class="tag_line">
    <a class="tags tag_stpwd" href="http://jiankang.163.com/special/zhutierji/?type=3">身体密码</a>
    </p>
    <div class="column_main">
    <a class="detail" href="https://jiankang.163.com/19/0625/11/EIH061CM0038804G.html" ne-role="detail">
    <h3>
                                    防晒，99%的人都做错了……
                                </h3>
    <div class="photo">
    <img alt="防晒，99%的人都做错了……" height="90" src="https://cms-bucket.ws.126.net/2019/06/25/f260b6843fca4702bb5e4e316600f113.png?imageView&amp;thumbnail=200y90" width="200"/>
    </div>
    </a>
    <ul>
    <li class=""><a href="https://jiankang.163.com/19/0617/14/EHSN7PPV0038804G.html">当代人减肥：迈不过25岁这道坎</a></li>
    <li class="twoli"><a href="https://jiankang.163.com/19/0608/15/EH5J9IGA00388AD5.html">多年后 无数中年人仍会被高考吓醒</a></li>
    </ul>
    </div>
    </li>
    <!-- 身体密码 结束 -->
    <!-- 哒哒 开始 -->
    <!-- 哒哒 结束 -->
    </ul>
    </div>
    <div id="js_baseline"></div>
    <span class="white_bg" id="js_white_bg"></span>
    </div>
    </div>
    </div>
    </div>
    <!-- 右侧960原创栏目 结束 -->
    <div class="mt12 mod_ad_1 mod_ad_r">
    <!-- 300*250 -->
    <div adtype="rightAd" class="at_item right_ad_item" requesturl="https://nex.163.com/q?app=7BE0FC82&amp;c=news&amp;l=31&amp;site=netease&amp;affiliate=news&amp;cat=homepage&amp;type=logo300x250&amp;location=1"></div>
    <a class="ad_hover_href" href="javascript:;" target="_self"></a>
    </div>
    <!-- 新闻策划 开始 -->
    <div class="mt35 mod_pageh5">
    <div ne-module="/news/index2016_rmd/modules/modh5/modh5.js">
    <div class="idx_cm_title">
    <a class="title" href="https://open.163.com/">网易公开课</a>
    </div>
    <div class="wrap" ne-module="/modules/slide/slide.js" ne-state="slideMethod:left;events=mouseover;interval=4000;loop=true;">
    <div class="h5_bg h5_border">
    <div class="h5_body" ne-role="slide-body">
    <div class="h5_main clearfix" ne-role="slide-scroll">
    <div class="h5_item" ne-role="slide-page">
    <div class="h5_item_poster">
    <a href="https://vip.open.163.com/courses/2698?p=xs_yt01">
    <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/b2ef8c1d0fed49078cb104f94c9f253e.jpeg" width="280"/>
    <span class="bg"></span>
    <h3>他凭什么甩开同龄人，做职场前5%？</h3>
    </a>
    </div>
    </div>
    <div class="h5_item" ne-role="slide-page">
    <div class="h5_item_poster">
    <a href="https://vip.open.163.com/courses/2249?p=xs_yt02">
    <img height="436" src="https://cms-bucket.ws.126.net/2019/06/27/ffa8db82492446c88efe2d540ed64d6a.jpeg" width="280"/>
    <span class="bg"></span>
    <h3>一个人成熟的标志：与负面情绪和解</h3>
    </a>
    </div>
    </div>
    <div class="h5_item" ne-role="slide-page">
    <div class="h5_item_poster">
    <a href="https://vip.open.163.com/courses/1078?p=xs_yt03">
    <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/893a6ecab816408cb5971de6ec236dde.jpeg" width="280"/>
    <span class="bg"></span>
    <h3>情商高的人，走到哪儿都大受欢迎</h3>
    </a>
    </div>
    </div>
    <div class="h5_item" ne-role="slide-page">
    <div class="h5_item_poster">
    <a href="https://vip.open.163.com/courses/2019?p=xs_yt04">
    <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/f48048d211e44c889e241e545b29a000.jpeg" width="280"/>
    <span class="bg"></span>
    <h3>每天5分钟，告别办公室综合症</h3>
    </a>
    </div>
    </div>
    </div>
    <span class="ad_hover_pic">广告</span>
    </div>
    <!-- <div class="scrollbtn scrollbtl" ne-role="scrollbtn"><a ne-role="slide-prev" class="f_prev">&lt;</a></div>
    		<div class="scrollbtn scrollbtnr" ne-role="scrollbtn"><a ne-role="slide-next" class="f_next">&gt;</a></div> -->
    <div class="nav clearfix">
    <span ne-repeat="1..state.total" ne-role="slide-nav"></span>
    </div>
    </div>
    <!-- <div class="nav clearfix">
    		<span ne-role="slide-nav" ne-repeat="1..state.total"></span>
    	</div> -->
    </div></div>
    </div>
    <!-- 新闻策划 结束 -->
    <!-- 新闻专题 开始 -->
    <div class="mt30 mod_news_special">
    <div class="idx_cm_title">
    <h2 class="title"><a href="http://news.163.com/special/">新闻专题</a></h2>
    </div>
    <div class="bd">
    <div class="photo">
    <a href="http://news.163.com/special/2019qglh/">
    <img alt="2019年全国两会" height="90" src="https://cms-bucket.ws.126.net/2019/03/07/c8134391d38245dc849b99fbf1ce33b0.png?imageView&amp;thumbnail=300y90" width="300"/>
    </a>
    </div>
    <h3>
    <span>HOT</span>
    <strong><a href="http://news.163.com/special/2019qglh/">2019年全国两会</a></strong>
    </h3>
    <ul class="idx_cm_list">
    <li>
    <a href="http://news.163.com/special/zghj70/">海军成立70周年</a>
    </li>
    <li>
    <a href="http://news.163.com/special/chunyun_2019/">2019年春运春节</a>
    </li>
    <li>
    <a href="http://news.163.com/special/chang_e4/">嫦娥四号登月</a>
    </li>
    <li>
    <a href="http://cms-bucket.ws.126.net/2019/06/26/080a0e9f8b014dd5b261f9e988f7f7f9.jpeg">声明</a>
    </li>
    </ul>
    </div>
    </div>
    <!-- 新闻专题 结束 -->
    <!-- 高层动态 开始-->
    <div class="mt27 mod_high_dynamic">
    <div class="idx_cm_title">
    <h2 class="title"><a href="http://news.163.com/special/00011269/gdmore.html">高层动态</a></h2>
    </div>
    <ul class="idx_cm_list idx_cm_list_h">
    <li>
    <a href="https://news.163.com/19/0628/11/EIOL0214000189FH.html">习近平会见联合国秘书长古特雷斯</a>
    </li>
    <li>
    <a href="https://news.163.com/19/0620/14/EI4ESVV9000189FH.html">习近平抵达平壤 开始对朝鲜进行国事访问</a>
    </li>
    </ul>
    </div>
    <!-- 高层动态 结束-->
    <div class="mt25 mod_ad_2 mod_ad_r">
    <!-- 300*250 -->
    <div adtype="rightAd" class="at_item right_ad_item" requesturl="https://nex.163.com/q?app=7BE0FC82&amp;c=news&amp;l=32&amp;site=netease&amp;affiliate=news&amp;cat=homepage&amp;type=logo300x250&amp;location=2"></div>
    <a class="ad_hover_href" href="javascript:;" target="_self"></a>
    </div>
    <!-- 军事 航空  开始 -->
    <div class="mt35 mod_war">
    <div class="idx_cm_title">
    <h2 class="title">
    <a href="http://war.163.com/">军事</a>
    <i>・</i>
    <a href="http://news.163.com/air/">航空</a>
    </h2>
    </div>
    <div class="idx_cm_img">
    <a href="http://war.163.com/photoview/4T8E0001/2301528.html">
    </a></div></div></div></div></div></div></div></div></body></html>



```python
samples = soup.find_all("a")
samples
```




    [<a class="ntes-nav-index-title ntes-nav-entry-wide c-fl" href="http://www.163.com/" title="网易首页">网易首页</a>,
     <a class="ntes-nav-select-title ntes-nav-entry-bgblack JS_NTES_LOG_FE" href="http://www.163.com/#f=topnav">应用
                 <em class="ntes-nav-select-arr"></em>
     </a>,
     <a href="http://m.163.com/newsapp/#f=topnav">
     <span>
     <em class="ntes-nav-app-newsapp">网易新闻</em>
     </span>
     </a>,
     <a href="http://open.163.com/#f=topnav">
     <span>
     <em class="ntes-nav-app-open">网易公开课</em>
     </span>
     </a>,
     <a href="https://hongcai.163.com/?from=pcsy-button">
     <span>
     <em class="ntes-nav-app-hongcai">网易红彩</em>
     </span>
     </a>,
     <a href="http://u.163.com/aosoutbdbd8">
     <span>
     <em class="ntes-nav-app-yanxuan">网易严选</em>
     </span>
     </a>,
     <a href="http://mail.163.com/client/dl.html?from=mail46">
     <span>
     <em class="ntes-nav-app-mail">邮箱大师</em>
     </span>
     </a>,
     <a href="http://study.163.com/client/download.htm?from=163app&amp;utm_source=163.com&amp;utm_medium=web_app&amp;utm_campaign=business">
     <span>
     <em class="ntes-nav-app-study">网易云课堂</em>
     </span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece47f92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=6b69bfbfac0db5f335232faa957a27bb&amp;target=https%3A%2F%2Fapp.kaola.com%2F%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>
     <em class="ntes-nav-app-kaola-hg">网易考拉</em>
     </span>
     </a>,
     <a class="ntes-nav-quick-navigation-btn" href="javascript:void(0);" id="js_N_ntes_nav_quick_navigation_btn" target="_self">
     <em>快速导航
                   <span class="menu1"></span>
     <span class="menu2"></span>
     <span class="menu3"></span>
     </em>
     </a>,
     <a href="https://news.163.com">新闻</a>,
     <a href="http://news.163.com/domestic">国内</a>,
     <a href="http://news.163.com/world">国际</a>,
     <a href="http://news.163.com/photo">图片</a>,
     <a href="http://view.163.com">评论</a>,
     <a href="http://discovery.163.com">探索</a>,
     <a href="http://war.163.com">军事</a>,
     <a href="http://news.163.com/localnews/">本地新闻</a>,
     <a href="http://news.163.com/special/wangsansanhome/">王三三</a>,
     <a href="http://sports.163.com">体育</a>,
     <a href="http://sports.163.com/nba">NBA</a>,
     <a href="http://sports.163.com/cba">CBA</a>,
     <a href="http://sports.163.com/allsports">综合</a>,
     <a href="http://sports.163.com/zc">中超</a>,
     <a href="http://sports.163.com/world">国际足球</a>,
     <a href="http://sports.163.com/yc">英超</a>,
     <a href="http://sports.163.com/xj">西甲</a>,
     <a href="http://sports.163.com/yj">意甲</a>,
     <a href="http://ent.163.com">娱乐</a>,
     <a href="http://ent.163.com/star">明星</a>,
     <a href="http://ent.163.com/photo">图片</a>,
     <a href="http://ent.163.com/movie">电影</a>,
     <a href="http://ent.163.com/tv">电视</a>,
     <a href="http://ent.163.com/music">音乐</a>,
     <a href="http://ent.163.com/special/gsbjb/">稿事编辑部</a>,
     <a href="http://ent.163.com/special/focus_ent/">娱乐FOCUS</a>,
     <a href="http://ent.163.com/special/xbkhz/">星捕快</a>,
     <a href="http://money.163.com">财经</a>,
     <a href="http://money.163.com/stock">股票</a>,
     <a href="http://quotes.money.163.com/stock">行情</a>,
     <a href="http://money.163.com/chanjing">产经</a>,
     <a href="http://money.163.com/ipo">新股</a>,
     <a href="http://money.163.com/finance">金融</a>,
     <a href="http://money.163.com/fund">基金</a>,
     <a href="http://biz.163.com">商业</a>,
     <a href="http://money.163.com/licai">理财</a>,
     <a href="http://auto.163.com">汽车</a>,
     <a href="http://auto.163.com/buy">购车</a>,
     <a href="http://auto.163.com/depreciate">行情</a>,
     <a href="http://product.auto.163.com/finder">选车</a>,
     <a href="http://product.auto.163.com">车型库</a>,
     <a href="http://auto.163.com/news">行业</a>,
     <a href="http://auto.163.com/chezhu">用车</a>,
     <a href="http://auto.163.com/photo">汽车图片</a>,
     <a href="http://tech.163.com">科技</a>,
     <a href="http://tech.163.com/telecom/">通信</a>,
     <a href="http://tech.163.com/it">IT</a>,
     <a href="http://tech.163.com/internet">互联网</a>,
     <a href="http://tech.163.com/special/ydhlw">移动互联网</a>,
     <a href="http://tech.163.com/special/chzt">特别策划</a>,
     <a href="http://tech.163.com/special/wudaokou">五道口沙龙</a>,
     <a href="http://tech.163.com/special/yyzd">易语中的</a>,
     <a href="http://tech.163.com/special">专题</a>,
     <a href="http://lady.163.com">女人</a>,
     <a href="http://baby.163.com">亲子</a>,
     <a href="http://fashion.163.com/art">艺术</a>,
     <a href="http://fashion.163.com">时尚</a>,
     <a href="http://shoucang.163.com">收藏</a>,
     <a href="http://lady.163.com/sense">情感</a>,
     <a href="http://lady.163.com/astro">星座</a>,
     <a href="http://lady.163.com/beauty">美容</a>,
     <a href="http://cosmetic.lady.163.com/trial">免费试用</a>,
     <a href="http://mobile.163.com">手机</a>,
     <a href="http://digi.163.com/">数码</a>,
     <a href="http://mobile.163.com/mi">移动</a>,
     <a href="http://digi.163.com/pc">电脑</a>,
     <a href="http://product.mobile.163.com">手机库</a>,
     <a href="http://hea.163.com/">家电</a>,
     <a href="http://digi.163.com/smart">智能硬件</a>,
     <a href="http://digi.163.com/dc">相机</a>,
     <a href="http://v.mobile.163.com">手机视频</a>,
     <a href="http://house.163.com">房产</a>,
     <a href="http://home.163.com">家居</a>,
     <a href="http://bj.house.163.com">北京房产</a>,
     <a href="http://sh.house.163.com">上海房产</a>,
     <a href="http://gz.house.163.com">广州房产</a>,
     <a href="http://house.163.com/city">全部分站</a>,
     <a href="http://xf.house.163.com">楼盘库</a>,
     <a href="http://home.163.com/jiaju/">家具</a>,
     <a href="http://home.163.com/weiyu/">卫浴</a>,
     <a href="http://home.163.com/special/jiajuyigui">衣柜</a>,
     <a href="http://travel.163.com">旅游</a>,
     <a href="http://travel.163.com/outdoor">户外</a>,
     <a href="http://guizhou.travel.163.com">贵州</a>,
     <a href="http://travel.163.com/food">美食</a>,
     <a href="http://jingdian.travel.163.com/domestic/1000066937">四川</a>,
     <a href="http://jingdian.travel.163.com">景点</a>,
     <a href="http://jingdian.travel.163.com/domestic/1000066944">新疆</a>,
     <a href="http://travel.163.com/special/travellist/#f=endnav">专题</a>,
     <a href="http://jingdian.travel.163.com/domestic/1000066926/#f=endnav">西藏</a>,
     <a href="http://edu.163.com">教育</a>,
     <a href="http://edu.163.com/yimin">移民</a>,
     <a href="http://edu.163.com/kaoyan">考研</a>,
     <a href="http://edu.163.com/liuxue">留学</a>,
     <a href="http://edu.163.com/special/official">公务员</a>,
     <a href="http://edu.163.com/en">外语</a>,
     <a href="http://kids.163.com">中小学</a>,
     <a href="http://edu.163.com/gaokao">高考</a>,
     <a href="http://daxue.163.com">校园</a>,
     <a href="http://sitemap.163.com/"><i></i>查看网易地图</a>,
     <a class="ntes-nav-login-title" href="http://reg.163.com/" id="js_N_nav_login_title">登录</a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-register" href="http://reg.email.163.com/mailregAll/reg0.jsp?from=163navi&amp;regPage=163">注册免费邮箱
                     <em class="ntes-nav-select-arr"></em>
     </a>,
     <a href="http://reg.vip.163.com/register.m?from=topnav">
     <span style="width:190px;">注册VIP邮箱（特权邮箱，付费）</span>
     </a>,
     <a href="http://mail.163.com/client/dl.html?from=mail46">
     <span style="width:190px;">免费下载网易官方手机邮箱应用</span>
     </a>,
     <a class="ntes-nav-entry-wide c-fl" id="js_N_navLogout" target="_self">安全退出</a>,
     <a class="ntes-nav-mobile-title ntes-nav-entry-bgblack" href="http://www.163.com/newsapp/#f=163nav">
     <em class="ntes-nav-entry-mobile">移动端</em>
     </a>,
     <a href="http://www.163.com/newsapp/#f=163nav">
     <img src="//static.ws.126.net/f2e/include/common_nav/images/topapp.jpg"/>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-huatian ntes-nav-entry-bgblack" href="https://open.163.com/" id="js_love_url">
     <em class="ntes-nav-entry-huatian">网易公开课</em>
     <em class="ntes-nav-select-arr"></em>
     <span class="ntes-nav-msg">
     <em class="ntes-nav-msg-num"></em>
     </span>
     </a>,
     <a href="https://vip.open.163.com">
     <span>付费精品</span>
     </a>,
     <a href="https://open.163.com/ted/">
     <span>TED</span>
     </a>,
     <a href="https://open.163.com/ocw/">
     <span>国际名校公开课</span>
     </a>,
     <a href="http://open.163.com/cuvocw/">
     <span>中国大学视频公开课</span>
     </a>,
     <a href="https://open.163.com/appreciation">
     <span>赏课</span>
     </a>,
     <a href="https://open.163.com/khan/">
     <span>可汗学院</span>
     </a>,
     <a href="http://open.163.com/special/appdownload_pc/">
     <span>下载公开课</span>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-kaola ntes-nav-entry-bgblack" href="http://da.kaola.com/redirect?t=5aaebece48792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=d638f275b1755320e845734e53e897ee&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505" id="js_kaola_url">
     <em class="ntes-nav-entry-kaola">网易考拉</em>
     <em class="ntes-nav-select-arr"></em>
     <span class="ntes-nav-msg ntes-nav-kaola-msg" id="js_N_navKaolaMsg">
     <em class="ntes-nav-msg-num"></em>
     </span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece48f92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=b3e224752b2cad85e9831e8c6cf7fbbd&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fbimaibangdan.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>1000元新人大礼包</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece49392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=fd8e43f4a20a26fbe60f7e7de1f17efe&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>新人专享进口好货</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece49392c01&amp;p=c901ea7c&amp;proId=1024&amp;code=21bcd5b595fc235cfd11e3e1cff14177&amp;target=https%3A%2F%2Factivity.kaola.com%2Factivity%2FflashSaleIndex%2Fshow.html%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>今日限时抢购</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece49792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=ecc40777cb2d68a3d9fb078b232f081d&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfyrzolcpagerz.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>营养保健</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece49b92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=0cdd5a920c768340ffc12eccd659341d&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fnewpc.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>个人洗护</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece4a392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=ee49a3a793f22e648ac616f5dab061dd&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjpwmb9zcpagesl.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>美容彩妆</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece4a792c00&amp;p=c901ea7c&amp;proId=1024&amp;code=6eb2598fd20963efc203a4e3fe88f4e2&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fmyxrq.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>母婴儿童</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece4ab92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=3946ce460ba655c11afac69855dfc02b&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Ffoodnewcustomers.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>环球美食</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece4af92c00&amp;p=c901ea7c&amp;proId=1024&amp;code=2eee7290051863737a434d44f3c0d46f&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fnewtalent.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>家居生活</span>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-lofter ntes-nav-entry-bgblack" href="http://you.163.com/?from=web_fc_menhu_xinrukou_1" id="js_lofter_icon_url">
     <em class="ntes-nav-entry-lofter">网易严选</em>
     <em class="ntes-nav-select-arr"></em>
     <span class="ntes-nav-msg" id="js_N_navLofterMsg">
     <em class="ntes-nav-msg-num"></em>
     </span>
     </a>,
     <a href="http://you.163.com/act/static/Fb2d1OZ714.html?from=web_fc_menhu_xinrukou_1">
     <span>888元现金券</span>
     </a>,
     <a href="http://you.163.com/manufacturer/list?from=web_fc_menhu_xinrukou_3">
     <span>品牌制造商爆款</span>
     </a>,
     <a href="http://you.163.com/item/recommend?from=web_fc_menhu_xinrukou_4">
     <span>999+人气好评品</span>
     </a>,
     <a href="http://you.163.com/flashSale/index?from=web_fc_menhu_xinrukou_5">
     <span>限时特惠</span>
     </a>,
     <a href="http://you.163.com/item/list?categoryId=1005000&amp;from=web_fc_menhu_xinrukou_7">
     <span>居家床品</span>
     </a>,
     <a href="http://you.163.com/item/list?categoryId=1005001&amp;from=web_fc_menhu_xinrukou_8">
     <span>精致餐厨</span>
     </a>,
     <a href="http://you.163.com/item/list?categoryId=1008000&amp;from=web_fc_menhu_xinrukou_9">
     <span>箱包鞋类</span>
     </a>,
     <a href="http://you.163.com/item/list?categoryId=1010000&amp;from=web_fc_menhu_xinrukou_10">
     <span>经典服饰</span>
     </a>,
     <a href="http://you.163.com/item/list?categoryId=1005002&amp;from=web_fc_menhu_xinrukou_11">
     <span>健康美食</span>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-money ntes-nav-entry-bgblack" href="http://pay.163.com/">
     <em class="ntes-nav-entry-money">支付</em>
     <em class="ntes-nav-select-arr"></em>
     </a>,
     <a href="http://pay.163.com/#f=topnav">
     <span>一卡通充值</span>
     </a>,
     <a href="http://ecard.163.com/script/index#f=topnav">
     <span>一卡通购买</span>
     </a>,
     <a href="https://k.163.com/?product=163&amp;trackid=01">
     <span>网易白金卡</span>
     </a>,
     <a href="https://epay.163.com/">
     <span>我的网易支付</span>
     </a>,
     <a href="https://3c.163.com/?from=wangyimenhu16">
     <span>网易智造</span>
     </a>,
     <a href="http://lq.163.com?from=neteasemoney">
     <span>网易来钱-借现金</span>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-cart ntes-nav-entry-bgblack" href="http://baoxian.163.com/car/?from=mhgwc">
     <em class="ntes-nav-entry-cart">电商</em>
     <em class="ntes-nav-select-arr"></em>
     </a>,
     <a href="http://you.163.com?from=web_in_wydaohang">
     <span>严选</span>
     </a>,
     <a href="http://lq.163.com?from=neteasebuy">
     <span>我要借钱</span>
     </a>,
     <a href="http://da.kaola.com/redirect?t=5aaebece4b392c00&amp;p=c901ea7c&amp;proId=1024&amp;code=d15f8f9d72ccc507aeefda91b43c0cd2&amp;target=https%3A%2F%2Fpages.kaola.com%2Fpages%2Factivity%2Fjfccri80pages1.shtml%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">
     <span>网易考拉</span>
     </a>,
     <a class="ntes-nav-select-title ntes-nav-select-title-mail ntes-nav-entry-bgblack" id="js_mail_url">
     <em class="ntes-nav-entry-mail">邮箱</em>
     <em class="ntes-nav-select-arr"></em>
     <span class="ntes-nav-msg" id="js_N_navMailMsg">
     <em class="ntes-nav-msg-num" id="js_N_navMailMsgNum"></em>
     </span>
     </a>,
     <a href="http://email.163.com/#f=topnav">
     <span>免费邮箱</span>
     </a>,
     <a href="http://vipmail.163.com/#f=topnav">
     <span>VIP邮箱</span>
     </a>,
     <a href="http://qiye.163.com/#f=topnav">
     <span>企业邮箱</span>
     </a>,
     <a href="http://reg.email.163.com/mailregAll/reg0.jsp?from=ntes_nav&amp;regPage=163">
     <span>免费注册</span>
     </a>,
     <a href="http://reg.email.163.com/unireg/call.do?cmd=register.entrance&amp;flow=mobile&amp;from=ntes_nav">
     <span>快速注册</span>
     </a>,
     <a href="http://mail.163.com/dashi/dlpro.html?from=mail46">
     <span>客户端下载</span>
     </a>,
     <a class="first" href="https://news.163.com/">新闻</a>,
     <a href="http://sports.163.com/">体育</a>,
     <a href="http://sports.163.com/nba/">NBA</a>,
     <a href="http://ent.163.com/">娱乐</a>,
     <a href="http://money.163.com/">财经</a>,
     <a href="http://money.163.com/stock/">股票</a>,
     <a href="http://auto.163.com/" id="_link_auto">汽车</a>,
     <a href="http://tech.163.com/">科技</a>,
     <a href="http://mobile.163.com/">手机</a>,
     <a href="http://digi.163.com/">数码</a>,
     <a href="http://lady.163.com/">女人</a>,
     <a href="http://v.163.com/">直播</a>,
     <a href="http://v.163.com/special/video/#tuijian">视频</a>,
     <a href="http://travel.163.com/">旅游</a>,
     <a href="http://house.163.com/" id="houseUrl">房产</a>,
     <a href="http://home.163.com/" id="homeUrl">家居</a>,
     <a href="http://edu.163.com/">教育</a>,
     <a href="http://book.163.com/">读书</a>,
     <a href="https://news.163.com/" id="_link_game">本地</a>,
     <a href="http://jiankang.163.com/">健康</a>,
     <a href="http://rd.da.netease.com/redirect?t=5802fb18cf033c80&amp;p=e17af55c&amp;proId=1024&amp;target=https%3A%2F%2Fwww.kaola.com%2F%3Ftag%3Dbe3d8d027a530881037ef01d304eb505">海淘</a>,
     <a class="last" href="http://art.163.com/">艺术</a>,
     <a class="channel2019_logo channel2019_news_logo" href="https://news.163.com/">网易新闻有态度</a>,
     <a href="http://news.163.com/weather/">
     <script ne-repeat="weather in weatherInfo" type="text/template">
                     <img class="ns-weather-icon" ne-src="http://static.ws.126.net/f2e/news/index2015/img/weather/<%=weather.icon%>">
                     <div class="ns-weather-text"><%=weather.weather%></div>
                     <div class="ns-weather-info"><%=weather.temp2%>°~<%=weather.temp1%>°</div>
                     <div class="ns-weather-city"><%=weather.city%></div>
                 </script>
     </a>,
     <a href="http://www.163.com/">首页</a>,
     <a href="http://news.163.com/rank/">排行</a>,
     <a href="http://news.163.com/photo/#Current">图片</a>,
     <a href="http://news.163.com/domestic/">国内</a>,
     <a href="http://news.163.com/world/">国际</a>,
     <a href="http://data.163.com/special/datablog/">数读</a>,
     <a href="http://war.163.com/">军事</a>,
     <a href="http://news.163.com/air/">航空</a>,
     <a href="http://news.163.com/uav/">无人机</a>,
     <a href="http://news.163.com/college">新闻学院</a>,
     <a href="http://gov.163.com/">政务</a>,
     <a href="http://gongyi.163.com/">公益</a>,
     <a href="http://media.163.com/">媒体</a>,
     <a href="http://news.163.com/special/wangsansanhome/">王三三</a>,
     <a class="tags tag_sd" href="http://data.163.com/special/datablog/">数读</a>,
     <a class="detail" href="http://data.163.com/19/0626/14/EIJQJG9L000181IU.html" ne-role="detail">
     <h3>
                                     中国哪里的地铁最拥挤？
                                 </h3>
     <div class="photo">
     <img alt="中国哪里的地铁最拥挤？" height="90" src="https://cms-bucket.ws.126.net/2019/06/26/30e8760df3044e29a18fac3514dd22b1.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://data.163.com/19/0625/11/EIH0CQEK00019GOE.html">娶一个潮汕老婆到底是什么体验</a>,
     <a href="http://data.163.com/19/0621/17/EI7BLS3600019GOE.html">不瞒你说，成都早餐好吃到爆</a>,
     <a class="tags tag_rj" href="http://renjian.163.com/">人间</a>,
     <a class="detail" href="http://renjian.163.com/19/0628/14/EIP21K41000181RV.html" ne-role="detail">
     <h3>
                                     小白作者的变现之路
                                 </h3>
     <div class="photo">
     <img alt="小白作者的变现之路" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/27f33fcbfcec4b42b6837807b7a0883f.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0627/16/EIML2HJO000181RV.html">被毒虫男友拖下水的女大学生</a>,
     <a href="http://renjian.163.com/19/0626/13/EIJPJMCH000181RV.html">领导，求你让我加班吧</a>,
     <a class="detail" href="http://renjian.163.com/19/0624/14/EIEOBNCB000181RK.html" ne-role="detail">
     <h3>
                                     当不了官发不了财的读书人
                                 </h3>
     <div class="photo">
     <img alt="当不了官发不了财的读书人" height="90" src="https://cms-bucket.ws.126.net/2019/06/24/b77e119ffeca477fa4bd2144b1fcb86c.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0620/16/EI4JRNO7000181RK.html">四个博士，一地鸡毛</a>,
     <a href="http://renjian.163.com/19/0618/12/EHV0QRVG000181RK.html">医闹得逞后，伤害的到底是谁</a>,
     <a class="detail" href="https://news.163.com/19/0627/11/EIM57O490001885B.html" ne-role="detail">
     <h3>
                                     据说99%的人在图书馆一定会碰上......
                                 </h3>
     <div class="photo">
     <img alt="据说99%的人在图书馆一定会碰上......" height="90" src="https://cms-bucket.ws.126.net/2019/06/27/06eb8f4a3d4647bf9360ff5e71f003b8.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0626/15/EIK0IJT40001885B.html">我可能，得了种，前任病</a>,
     <a href="https://news.163.com/19/0617/09/EHS57H4L0001885B.html">那些KO不掉我的,最终成了我的OK</a>,
     <a class="detail" href="https://news.163.com/19/0628/11/EIOL94760001885B.html" ne-role="detail">
     <h3>
                                     直男幼稚行为大赏
                                 </h3>
     <div class="photo">
     <img alt="直男幼稚行为大赏" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/0b3890cd2f4b473fa0127b5e33ae6ccf.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0624/12/EIEFGMVL0001885B.html">打个赌，爱情友情你分不清楚</a>,
     <a href="https://news.163.com/19/0621/12/EI6NKDTU0001885B.html">不会唱歌的人进 KTV 以后有多惨</a>,
     <a class="detail" href="https://news.163.com/19/0628/19/EIPIQT4O000181BR.html" ne-role="detail">
     <h3>
                                     彩票一直都不中，我却忍不住要买
                                 </h3>
     <div class="photo">
     <img alt="彩票一直都不中，我却忍不住要买" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f44265c5b4ef4a11a99eedbde7c49833.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0627/17/EIMPGJAU000181BR.html">原来"神仙眷侣"离婚,也是一地鸡毛</a>,
     <a href="https://news.163.com/19/0626/18/EIK95RV0000181BR.html">我宣布，北大清华这对CP锁死了！</a>,
     <a class="detail" href="http://caozhi.news.163.com/19/0623/22/EID0CBIH000181TI.html" ne-role="detail">
     <h3>
                                     佟丽娅，这次你赢了
                                 </h3>
     <div class="photo">
     <img alt="佟丽娅，这次你赢了" height="90" src="https://cms-bucket.ws.126.net/2019/06/23/67d24242d479451ea705e26296187f78.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://caozhi.news.163.com/19/0623/15/EIC9LGSP000181TI.html">千万别在深夜点开这神作</a>,
     <a href="http://caozhi.news.163.com/19/0618/19/EHVRID7G000181TI.html">那个发“嗯”的人，已被踢出群聊</a>,
     <a class="detail" href="https://news.163.com/19/0628/17/EIPCOKEA0001982T.html" ne-role="detail">
     <h3>
                                     王宝强母亲去世：来日方长是人生的错觉
                                 </h3>
     <div class="photo">
     <img alt="王宝强母亲去世：来日方长是人生的错觉" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/ecd0de8b8dc0402da72d814bde76f06e.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0627/13/EIMC0EDH0001982T.html">宋仲基宋慧乔离婚：再美的爱情也会过期</a>,
     <a href="https://news.163.com/19/0626/17/EIK6AD550001982T.html">杨紫冰箱藏药，戳穿最怂瞬间</a>,
     <a class="tags tag_kanke" href="http://renjian.163.com/special/renjian_kanke/">看客</a>,
     <a class="detail" href="http://renjian.163.com/19/0628/11/EIOMK185000199ET.html" ne-role="detail">
     <h3>
                                     我奶茶都戒了，日本人才知道它的好
                                 </h3>
     <div class="photo">
     <img alt="我奶茶都戒了，日本人才知道它的好" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f35eceb8d111496693e8f77a71a49cba.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0620/11/EI43PM8Q000199ET.html">美国堕胎残酷物语</a>,
     <a href="http://renjian.163.com/19/0613/11/EHI39FML000199ET.html">跑腿小哥提供的十万种服务</a>,
     <a class="tags tag_stpwd" href="http://jiankang.163.com/special/zhutierji/?type=3">身体密码</a>,
     <a class="detail" href="https://jiankang.163.com/19/0625/11/EIH061CM0038804G.html" ne-role="detail">
     <h3>
                                     防晒，99%的人都做错了……
                                 </h3>
     <div class="photo">
     <img alt="防晒，99%的人都做错了……" height="90" src="https://cms-bucket.ws.126.net/2019/06/25/f260b6843fca4702bb5e4e316600f113.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://jiankang.163.com/19/0617/14/EHSN7PPV0038804G.html">当代人减肥：迈不过25岁这道坎</a>,
     <a href="https://jiankang.163.com/19/0608/15/EH5J9IGA00388AD5.html">多年后 无数中年人仍会被高考吓醒</a>,
     <a href="https://news.163.com/19/0628/16/EIP8R4SV000189FH.html">央视独家：习近平会见日本首相</a>,
     <a href="https://news.163.com/19/0628/16/EIP8N52U0001875N.html">外交部回应中美元首会面</a>,
     <a href="https://news.163.com/19/0628/14/EIOVIP2500018AP1.html" target="_blank">特朗普会见普京 笑称:不要干预美国大选哦</a>,
     <a href="https://news.163.com/19/0628/16/EIP7KOH70001875P.html">住建部:加快垃圾分类处理设施建设</a>,
     <a href="https://news.163.com/19/0628/16/EIP8F9QQ0001875P.html" target="_blank">袁仁国被公诉:受贿数额特别巨大</a>,
     <a href="https://news.163.com/19/0628/13/EIOSPGLJ0001899O.html">湖南耒阳人大常委会原主任携子主动投案</a>,
     <a href="https://news.163.com/19/0628/13/EIOUHOB70001875P.html" target="_blank">美的48小时内被骗10亿资金</a>,
     <a href="https://news.163.com/19/0628/19/EIPH3F1V0001875P.html">垃圾分类逼疯上海人？别笑！马上轮到这46个城市</a>,
     <a href="https://news.163.com/19/0628/19/EIPILCJ70001875P.html">女子酒后澡堂一打六被刑拘</a>,
     <a href="https://news.163.com/19/0628/18/EIPFI0KN0001875P.html" target="_blank">杀人案嫌犯向警察开枪拒捕 被当场击毙</a>,
     <a href="https://news.163.com/19/0628/16/EIP8RHM70001875P.html">95后飙摩托车追高铁发抖音被刑拘</a>,
     <a href="https://news.163.com/19/0628/16/EIP7B7RP0001899O.html" target="_blank">母亲担心儿子粗心在其手背"刺"字</a>,
     <a href="https://news.163.com/19/0628/15/EIP4Q6BQ0001899O.html">女子高铁上劝老人看好小孩被骂</a>,
     <a href="https://news.163.com/19/0628/16/EIP8QO5Q0001875P.html" target="_blank">南京杀妻案死者姑妈：侄女生前要强</a>,
     <a class="ad_hover_href" href="http://gb.corp.163.com/gb/legal.html"></a>,
     <a href="http://news.163.com/16/0721/19/BSH7V8QF00014JB6.html">辽宁遭暴雨侵袭致城市内涝 紧急转移12万人</a>,
     <a href="http://news.163.com/16/0721/10/BSG7HOH20001124J.html">民政部:北方暴雨75人死亡失踪</a>,
     <a href="http://news.163.com/16/0721/12/BSGG5VK300011229.html" target="_blank">北京发生山洪灾害 铲车翻倒4人被困</a>,
     <a href="http://news.163.com/16/0721/12/BSGHHVLK00011229.html">搜救犬水灾救援22天殉职 主人:它太累了</a>,
     <a href="http://news.163.com/16/0721/07/BSFUFFP800014AED.html" target="_blank">姐妹被洪水卷走警方拒立案</a>,
     <a href="http://news.163.com/photoview/00AN0001/2189402.html?from=ph_ss#p=BSG716GE00AN0001">
     <img height="120" src="http://img3.cache.netease.com/news/2016/7/21/20160721131401d35e2.jpg" width="190"/>
     <span class="bg"></span>
     <h3>河南遇强降雨 9.8万人转移</h3>
     </a>,
     <a href="http://news.163.com/photoview/00AP0001/2189377.html?from=ph_ss#p=BSFTQ99H00AP0001">
     <img height="120" src="http://img3.cache.netease.com/news/2016/7/21/201607211319466e84e.jpg" width="190"/>
     <span class="bg"></span>
     <h3>女主播直播暴雨 浑身湿透</h3>
     </a>,
     <a href="http://news.163.com/photoview/00AP0001/2189389.html?from=ph_ss#p=BSG1S9AM00AP0001">
     <img height="120" src="http://img5.cache.netease.com/news/2016/7/21/20160721132119ef59b.jpg" width="190"/>
     <span class="bg"></span>
     <h3>湖北民众省道上趟水摸鱼</h3>
     </a>,
     <a href="https://open.163.com/">网易公开课</a>,
     <a class="focus_prev" ne-role="slide-prev"></a>,
     <a class="focus_next" ne-role="slide-next"></a>,
     <a class="nav_name no_cursor" href="javascript:;" ne-role="tab-nav" target="_self">
                         要闻
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name no_cursor" href="{{myState.channelbendiurl}}" ne-class="{{myState.bendiTstyle ? 'bendistyle' : ''}}" ne-role="tab-nav" target="{{myState.channelbendiurl == 'javascript:;' ? '_self' : '_blank'}}">
     <strong ne-text="{{myState.bendiCity}}"></strong>
     <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name" href="http://news.163.com/domestic/" ne-role="tab-nav">
                         国内
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name" href="http://news.163.com/world/" ne-role="tab-nav">
                         国际
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name no_cursor" href="javascript:;" ne-role="tab-nav" target="_self">
                         独家
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name" href="http://war.163.com/" ne-role="tab-nav">
                         军事
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name" href="http://money.163.com/" ne-role="tab-nav">
                         财经
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="nav_name" href="http://tech.163.com/" ne-role="tab-nav">
                         科技
                         <span class="nav_item_ink"></span>
     </a>,
     <a class="more" href="javascript:;" ne-class="{{myState.morechannel ? 'more_hover': ''}}" ne-mouseout="morehideChannel()" ne-mouseover="moreShowChannel()" ne-role="morebtn" target="_self">更多</a>,
     <a href="http://sports.163.com/" ne-role="tab-nav">体育</a>,
     <a href="http://ent.163.com/" ne-role="tab-nav">娱乐</a>,
     <a href="http://lady.163.com/" ne-role="tab-nav">时尚</a>,
     <a href="http://auto.163.com/" ne-role="tab-nav">汽车</a>,
     <a href="{{myState.channelhouseurl}}" ne-role="tab-nav">房产</a>,
     <a href="http://news.163.com/air/" ne-role="tab-nav">航空</a>,
     <a href="http://jiankang.163.com/" ne-role="tab-nav">健康</a>,
     <a class="newsdata_prev" href="#prev" ne-class="{{myState.fixedTop ? 'fixed_data_show': ''}}" ne-click="tabPrevFn($event);" ne-hide="{{myState.iPad}}">
     <span></span>
     <div class="newsdata_btn_name">{{myState.preBtnName}}</div>
     </a>,
     <a class="newsdata_next" href="#next" ne-class="{{myState.fixedTop ? 'fixed_data_show': ''}}" ne-click="tabNextFn($event);" ne-hide="{{myState.iPad}}">
     <span></span>
     <div class="newsdata_btn_name">{{myState.nextBtnName}}</div>
     </a>,
     <a class="load_more_btn" ne-click="clickLoadMore();" ne-hide="{{myState.counter &gt;= navList[myState.ndNavIndex].totalPage || myState.counter == 0}}" target="_self">
     <div class="post_addmore" ne-visible="{{myState.counter &lt; navList[myState.ndNavIndex].totalPage &amp;&amp; !myState.loading}}">
     <i>+</i>
     <span>加载更多</span>
     </div>
     <div class="post_adding" ne-show="{{myState.loading}}">
     <i>+</i>
     <span>加载中...</span>
     </div>
     </a>,
     <a href="http://g.163.com/a?CID=68685&amp;Values=1366894002&amp;Redirect=http://clk.gentags.net/clk/iv-10648/st-31/cr-2/oi-1303641/or-7535/adv-158/pcon-0/https%253A%252F%252Fent.163.com%252F19%252F0625%252F16%252FEIHG8HLF000398QL.html">
     <img height="400" src="http://nimg.ws.126.net/?url=https://yt-adp.ws.126.net/channel21/037408_300400_axry_20190626.jpg&amp;thumbnail=300x2147483647&amp;quality=75&amp;type=jpg" width="300"/>
     <span class="bg"></span>
     <h3>三金西瓜霜独家冠名网易封面故事</h3>
     </a>,
     <a href="http://news.163.com/photoview/00AP0001/2302561.html">
     <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/e5b070c1f96349b0829da88b41105903.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
     <span class="bg"></span>
     <h3>浒苔绿潮开始在山东沿海登陆</h3>
     </a>,
     <a href="http://news.163.com/photoview/00AP0001/2302559.html">
     <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/2792654fe66f4985879a8cc30a89a6cc.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
     <span class="bg"></span>
     <h3>广西南宁抓获涉传人员286名</h3>
     </a>,
     <a href="http://news.163.com/photoview/00AO0001/2302560.html">
     <img height="400" src="https://cms-bucket.ws.126.net/2019/06/28/202e20527525474cac861ba7e56a2dde.jpeg?imageView&amp;thumbnail=300y400" width="300"/>
     <span class="bg"></span>
     <h3>民主党初选辩论次日:拜登现身</h3>
     </a>,
     <a class="f_prev" ne-role="slide-prev">&lt;</a>,
     <a class="f_next" ne-role="slide-next">&gt;</a>,
     <a href="http://baoxian.163.com/activity/act1605/index.html?from=mhds1605">免费领取iPhone6s</a>,
     <a href="http://mall.163.com/mobile/fill.jsp?from=wwwtext">手机费快充超低折扣</a>,
     <a href="http://baoxian.163.com/car/activitylist.html?from=mhdstbl">免费送现金红包！</a>,
     <a href="http://piao.163.com/movie/47080.html?from=newsword">镜中多奇境依旧爱丽丝</a>,
     <a class="tags tag_sd" href="http://data.163.com/special/datablog/">数读</a>,
     <a class="detail" href="http://data.163.com/19/0626/14/EIJQJG9L000181IU.html" ne-role="detail">
     <h3>
                                     中国哪里的地铁最拥挤？
                                 </h3>
     <div class="photo">
     <img alt="中国哪里的地铁最拥挤？" height="90" src="https://cms-bucket.ws.126.net/2019/06/26/30e8760df3044e29a18fac3514dd22b1.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://data.163.com/19/0625/11/EIH0CQEK00019GOE.html">娶一个潮汕老婆到底是什么体验</a>,
     <a href="http://data.163.com/19/0621/17/EI7BLS3600019GOE.html">不瞒你说，成都早餐好吃到爆</a>,
     <a class="tags tag_rj" href="http://renjian.163.com/">人间</a>,
     <a class="detail" href="http://renjian.163.com/19/0628/14/EIP21K41000181RV.html" ne-role="detail">
     <h3>
                                     小白作者的变现之路
                                 </h3>
     <div class="photo">
     <img alt="小白作者的变现之路" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/27f33fcbfcec4b42b6837807b7a0883f.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0627/16/EIML2HJO000181RV.html">被毒虫男友拖下水的女大学生</a>,
     <a href="http://renjian.163.com/19/0626/13/EIJPJMCH000181RV.html">领导，求你让我加班吧</a>,
     <a class="detail" href="http://renjian.163.com/19/0624/14/EIEOBNCB000181RK.html" ne-role="detail">
     <h3>
                                     当不了官发不了财的读书人
                                 </h3>
     <div class="photo">
     <img alt="当不了官发不了财的读书人" height="90" src="https://cms-bucket.ws.126.net/2019/06/24/b77e119ffeca477fa4bd2144b1fcb86c.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0620/16/EI4JRNO7000181RK.html">四个博士，一地鸡毛</a>,
     <a href="http://renjian.163.com/19/0618/12/EHV0QRVG000181RK.html">医闹得逞后，伤害的到底是谁</a>,
     <a class="detail" href="https://news.163.com/19/0627/11/EIM57O490001885B.html" ne-role="detail">
     <h3>
                                     据说99%的人在图书馆一定会碰上......
                                 </h3>
     <div class="photo">
     <img alt="据说99%的人在图书馆一定会碰上......" height="90" src="https://cms-bucket.ws.126.net/2019/06/27/06eb8f4a3d4647bf9360ff5e71f003b8.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0626/15/EIK0IJT40001885B.html">我可能，得了种，前任病</a>,
     <a href="https://news.163.com/19/0617/09/EHS57H4L0001885B.html">那些KO不掉我的,最终成了我的OK</a>,
     <a class="detail" href="https://news.163.com/19/0628/11/EIOL94760001885B.html" ne-role="detail">
     <h3>
                                     直男幼稚行为大赏
                                 </h3>
     <div class="photo">
     <img alt="直男幼稚行为大赏" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/0b3890cd2f4b473fa0127b5e33ae6ccf.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0624/12/EIEFGMVL0001885B.html">打个赌，爱情友情你分不清楚</a>,
     <a href="https://news.163.com/19/0621/12/EI6NKDTU0001885B.html">不会唱歌的人进 KTV 以后有多惨</a>,
     <a class="detail" href="https://news.163.com/19/0628/19/EIPIQT4O000181BR.html" ne-role="detail">
     <h3>
                                     彩票一直都不中，我却忍不住要买
                                 </h3>
     <div class="photo">
     <img alt="彩票一直都不中，我却忍不住要买" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f44265c5b4ef4a11a99eedbde7c49833.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0627/17/EIMPGJAU000181BR.html">原来"神仙眷侣"离婚,也是一地鸡毛</a>,
     <a href="https://news.163.com/19/0626/18/EIK95RV0000181BR.html">我宣布，北大清华这对CP锁死了！</a>,
     <a class="detail" href="http://caozhi.news.163.com/19/0623/22/EID0CBIH000181TI.html" ne-role="detail">
     <h3>
                                     佟丽娅，这次你赢了
                                 </h3>
     <div class="photo">
     <img alt="佟丽娅，这次你赢了" height="90" src="https://cms-bucket.ws.126.net/2019/06/23/67d24242d479451ea705e26296187f78.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://caozhi.news.163.com/19/0623/15/EIC9LGSP000181TI.html">千万别在深夜点开这神作</a>,
     <a href="http://caozhi.news.163.com/19/0618/19/EHVRID7G000181TI.html">那个发“嗯”的人，已被踢出群聊</a>,
     <a class="detail" href="https://news.163.com/19/0628/17/EIPCOKEA0001982T.html" ne-role="detail">
     <h3>
                                     王宝强母亲去世：来日方长是人生的错觉
                                 </h3>
     <div class="photo">
     <img alt="王宝强母亲去世：来日方长是人生的错觉" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/ecd0de8b8dc0402da72d814bde76f06e.jpeg?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://news.163.com/19/0627/13/EIMC0EDH0001982T.html">宋仲基宋慧乔离婚：再美的爱情也会过期</a>,
     <a href="https://news.163.com/19/0626/17/EIK6AD550001982T.html">杨紫冰箱藏药，戳穿最怂瞬间</a>,
     <a class="tags tag_kanke" href="http://renjian.163.com/special/renjian_kanke/">看客</a>,
     <a class="detail" href="http://renjian.163.com/19/0628/11/EIOMK185000199ET.html" ne-role="detail">
     <h3>
                                     我奶茶都戒了，日本人才知道它的好
                                 </h3>
     <div class="photo">
     <img alt="我奶茶都戒了，日本人才知道它的好" height="90" src="https://cms-bucket.ws.126.net/2019/06/28/f35eceb8d111496693e8f77a71a49cba.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="http://renjian.163.com/19/0620/11/EI43PM8Q000199ET.html">美国堕胎残酷物语</a>,
     <a href="http://renjian.163.com/19/0613/11/EHI39FML000199ET.html">跑腿小哥提供的十万种服务</a>,
     <a class="tags tag_stpwd" href="http://jiankang.163.com/special/zhutierji/?type=3">身体密码</a>,
     <a class="detail" href="https://jiankang.163.com/19/0625/11/EIH061CM0038804G.html" ne-role="detail">
     <h3>
                                     防晒，99%的人都做错了……
                                 </h3>
     <div class="photo">
     <img alt="防晒，99%的人都做错了……" height="90" src="https://cms-bucket.ws.126.net/2019/06/25/f260b6843fca4702bb5e4e316600f113.png?imageView&amp;thumbnail=200y90" width="200"/>
     </div>
     </a>,
     <a href="https://jiankang.163.com/19/0617/14/EHSN7PPV0038804G.html">当代人减肥：迈不过25岁这道坎</a>,
     <a href="https://jiankang.163.com/19/0608/15/EH5J9IGA00388AD5.html">多年后 无数中年人仍会被高考吓醒</a>,
     <a class="ad_hover_href" href="javascript:;" target="_self"></a>,
     <a class="title" href="https://open.163.com/">网易公开课</a>,
     <a href="https://vip.open.163.com/courses/2698?p=xs_yt01">
     <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/b2ef8c1d0fed49078cb104f94c9f253e.jpeg" width="280"/>
     <span class="bg"></span>
     <h3>他凭什么甩开同龄人，做职场前5%？</h3>
     </a>,
     <a href="https://vip.open.163.com/courses/2249?p=xs_yt02">
     <img height="436" src="https://cms-bucket.ws.126.net/2019/06/27/ffa8db82492446c88efe2d540ed64d6a.jpeg" width="280"/>
     <span class="bg"></span>
     <h3>一个人成熟的标志：与负面情绪和解</h3>
     </a>,
     <a href="https://vip.open.163.com/courses/1078?p=xs_yt03">
     <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/893a6ecab816408cb5971de6ec236dde.jpeg" width="280"/>
     <span class="bg"></span>
     <h3>情商高的人，走到哪儿都大受欢迎</h3>
     </a>,
     <a href="https://vip.open.163.com/courses/2019?p=xs_yt04">
     <img height="436" src="https://cms-bucket.ws.126.net/2019/06/26/f48048d211e44c889e241e545b29a000.jpeg" width="280"/>
     <span class="bg"></span>
     <h3>每天5分钟，告别办公室综合症</h3>
     </a>,
     <a href="http://news.163.com/special/">新闻专题</a>,
     <a href="http://news.163.com/special/2019qglh/">
     <img alt="2019年全国两会" height="90" src="https://cms-bucket.ws.126.net/2019/03/07/c8134391d38245dc849b99fbf1ce33b0.png?imageView&amp;thumbnail=300y90" width="300"/>
     </a>,
     <a href="http://news.163.com/special/2019qglh/">2019年全国两会</a>,
     <a href="http://news.163.com/special/zghj70/">海军成立70周年</a>,
     <a href="http://news.163.com/special/chunyun_2019/">2019年春运春节</a>,
     <a href="http://news.163.com/special/chang_e4/">嫦娥四号登月</a>,
     <a href="http://cms-bucket.ws.126.net/2019/06/26/080a0e9f8b014dd5b261f9e988f7f7f9.jpeg">声明</a>,
     <a href="http://news.163.com/special/00011269/gdmore.html">高层动态</a>,
     <a href="https://news.163.com/19/0628/11/EIOL0214000189FH.html">习近平会见联合国秘书长古特雷斯</a>,
     <a href="https://news.163.com/19/0620/14/EI4ESVV9000189FH.html">习近平抵达平壤 开始对朝鲜进行国事访问</a>,
     <a class="ad_hover_href" href="javascript:;" target="_self"></a>,
     <a href="http://war.163.com/">军事</a>,
     <a href="http://news.163.com/air/">航空</a>,
     <a href="http://war.163.com/photoview/4T8E0001/2301528.html">
     </a>]



> 参考：

1. [廖雪峰Python数据分析](https://www.julyedu.com/course/getDetail/66/)
