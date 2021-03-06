---
layout:     post
title:      移动互联网广告作弊初探
subtitle:   大家都知道的广告作弊的那些事儿
date:       2020-05-30
author:     Lance
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - 互联网广告作弊
---

## 前言

进入移动互联网时代，移动广告给产品带来无限的曝光量，给广告主带来流量上的巨大收益的同时，广告作弊的潜在威胁也深深的影响到了移动广告行业的运作。广告作弊这个词看起来很陌生，但是千万不要认为广告作弊离我们很远，其实它处处在我们生活中存在。毫无疑问，防范与抵制广告作弊，已然成为一场没有硝烟的战争。为了打好这场漫长的攻坚战，我们就需要充分的了解广告作弊的那些事儿 。

## 能够作弊的环节：

* 在正式介绍广告作弊之前，我们先来快速过一下广告投放的全过程，看看作弊都可能存在于哪些环节:

<div align="center"> <img src="http://liuyuabnn.github.io/img/ttou.jpg"/> </div><br>

* 广告主与媒体或代理商签订广告合同，约定结算方式并提供广告创意。主要结算方式有：CPM,CPC,CPA。

* 广告市场中往往有第三方统计SDK来监测广告效果，保障广告主的投入产出比。第三方会在广告展示/点击、激活环节添加检测代码/SDK，随着广告一齐到达用户端，进行效果归因(Attribution)。

* 媒体展示广告，用户看到广告创意并产生广告交互行为(展示、点击、下载和注册等)。在第三方代码的控制下，这些行为连带用户信息一齐被发送第三方进行统计。

* 第三方将统计得到的数据报表交给广告主，广告主凭借这份数据与媒体按照指标进行结算。

*广告的逻辑和流程都挺透明公开的，似乎没有什么可以作弊的地方，究竟是哪里出了问题呢?在广告中，要想理清业务的脉络，跟着钱的流向走准没错。以CPM为例，广告主按照第三方提供的曝光数据与媒体进行结算，而第三方的数据来源于用户端接收到的广告展示，广告展示又是通过第三方的检测代码统计来的。从数据到展示，从展示到检测代码。只要检测代码认为广告确实被展示了一次，那么不管该用户是否真的见到了广告，广告主都要为此次曝光付费。所谓作弊，就是一个让代码说谎的手段。*


## 谁会去作弊？

**媒体作弊**

>这个很容易理解，制造假流量创造更多的收入:

* 作弊第三方广告平台或者自己的直投广告主

**第三方广告平台作弊**

>广告主往往会对广告代理、DSP等提出量和质的要求，那要是达不到怎么办呢：

* 为了广告主的KPI作弊自己的广告主或者其他上游渠道

* 为了增加自己的收益作弊其他第三方广告平台(聚合广告)


**广告主自己竞争对手作弊**

>按CPM/CPC结算时，广告主如果得罪了谁，人家有可能盯着你的广告猛刷猛点，让你的预算耗尽还全无效果。当然，猛刷猛点需要骗过各个环节的反作弊系统才行。

* 消耗掉竞争对手的预算,自己的低价才能够胜出。

**广告主自己作弊**

>这个其实也不难理解，为了把数据做好看一点儿，获得平台排名上的优势，进而获得更多的自然量。

* ASO优化

---


## 移动端作弊的主要分类

**CPM/CPC作弊:**

* CPC/CPM的检测一般是个HTTP请求，它由在客户端监测代码所触发。监测代码的主要工作，是将客户端的信息以参数的形式拼凑成URL，并以HTTP请求的方式传给第三方，告知“谁，在什么时候，看到了来自哪个媒体展示的，哪个广告主的广告”。以移动端为例，常见的客户端参数有如下几种：

<div align="center"> <img src="http://liuyuabnn.github.io/img/cpm.jpg"/> </div><br>

>http://www.xxxxx.com/impCID=ad20&CPID=1321&CRID=20&OS=1&IDFA=70E0E6465B7B12C844C63EC681C7507C
&OpenUDID=F1C7976BC455CB548BFC550EB7687F06&IP=10.26.78.45&UA=iPhone;%20CPU%20iPhone
%20OS%206_1_2%20like%20Mac%20OS%20X)%20AppleWebKit/536.26%20(KHTML,%20like%20Gecko
&TS=1198628984102
>

* 既然是个URL，那么我们直接在服务器或者客户端直接请求这个地址，是不是也就在广告主那里记录了一个曝光呢?是的，这就是作弊刷量最朴素的哲学原理。CPC也是一样的!另外，不论是服务器刷还是客户端刷，在点击环节都会有个破绽：正常用户在点击广告时，自然的点击分布与广告创意有关，而刷的点击要么较为集中，要么均匀散布，并不难以分辨。那么作弊者么们都是如何触发这段代码的呢？

<div align="center"> <img src="http://liuyuabnn.github.io/img/click.png"/> </div><br>

* 点击优化：

	* 在广告素材展示View的上层展示一个“点我”。

    * 设置概率跳过按钮不生效，点击跳过相当于点击广告

* Hook第三方广告sdk监测代码：

	* 从填充到曝光之间有一个曝光成功率，那损失的一部分曝光去哪里了？可否让广告sdk说假话，让这一部分也曝光了呢。

	* 可否绕过第三方广告平台的包名验证机制,同时支持跑多个媒体。
	
* 破解第三方广告sdk协议

	* 主动往第三方服务器拿广告，并处理response数据。作弊成本较高，需要工匠精神

---


**CPA作弊**

>如何让广告主和第三方数据平台统计到激活数据（归因）：

* 所谓归因(Attribution)，通俗点的解释就是，到底是什么因素，最终导致了目标的达成。举个简单的例子。足球场上，A一脚射门进了，A说球是我进的，荣誉是我的。但是，A的球是B传给他的，不传球他也不会进球，所以B说他也有功劳。这时食堂做饭的大妈说了，都是我给你们营养调的好，你们才身体倍棒，所以这功劳也有我一份。综上，这个球应该归谁呢?常理上来说，这份荣誉人人都有;但是实际上，是A抢夺了B的传球贡献，也抢夺了食堂大妈的做饭贡献，独自一人享受进球荣誉，这就是归因。

* 归因作弊，是一种钻移动应用下载监测逻辑的空子而产生的作弊手段。在移动应用下载广告中，第三方监测一般规定：用户点击广告后一段时间内，产生的下载行为算作广告效果。那么是怎么统计这个广告效果的呢？
* 国内：一般采用用户ID碰撞归因。即广告sdk只能监测到点击，下载，安装完成这些行为，并把产生这些行为时客户端的设备环境参数上报，等被安装的App打开时，App内部集成的第三方统计平台会记录一次激活，并把这个激活的数据和之前广告sdk上报的参数做设备ID模糊匹配。当匹配上时，记录一次归因。

* 海外：Referrer： 广告点击链接会经过n次重定向（n-1次为第三方数据平台），最终跳转的地址是Google play。例如：

>	 https://play.google.com/store/apps/details? id=com.peitor.photoeditor&
referrer=adjust_reftag%3Dc7oYKoR43NYC1%26utm_source%3DPhotoEditor2017_ocean_2%26utm_campaign%3Dch1006

	<receiver android:name="com.google.android.gms.analytics.CampaignTrackingReceiver"
        android:enabled="true"
        android:exported="true">
        <intent-filter>
            <action android:name="com.android.vending.INSTALL_REFERRER" />
        </intent-filter>
    </receiver>


* 归因劫持：
	* 自然量劫持
	* 其他渠道归因劫持

>	implementation 'com.android.installreferrer:installreferrer:1.1'
	
	ReferrerDetails response = referrerClient.getInstallReferrer();
    String referrerUrl = response.getInstallReferrer();
    long referrerClickTime = response.getReferrerClickTimestampSeconds();
    long appInstallTime = response.getInstallBeginTimestampSeconds();
    boolean instantExperienceLaunched = response.getGooglePlayInstantParam();

* 虚假流量（NTH）:
	* 直接破解第三方数据平台协议。
        * 刷流量归因，日活，3日留存，7日留存，15日留存。

---

**人工作弊/机器作弊**

>刷机墙是一种简单粗暴的作弊手段，指的是同时操作多部手机终端，以人工或自动的方式，批量的刷各种转化。

* 机器行为

	* IP重复刷量、换不同IP重复刷量。

* 真人水军作弊

	* 引导用户完成某些指定操作。
	
---


## 作弊后记

* 后续效果好的渠道并不一定不是作弊渠道，抢来的金子也是金子。
 
* 作弊不是个局部性问题，某些市场的作弊比例可能高达80%以上。
 
* 我们并不能只靠数据统计就能很好的对抗作弊，不了解作弊的方法，防范作弊的成本就会大大提高。

* 无法一劳永逸的搭建一套成熟有效的反作弊系统，因为作弊和反作弊的博弈属性决定了斗争的长期性和动态性。

### 参考：

- [北冥乘海生](http://mp.weixin.qq.com/s/ss_jsOJ9Etp9obwRGEsvgw)
