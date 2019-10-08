title: 七喜官网
date: 2019-06-27 14:11:20
description: 
categories:
- CSS
tags:
- CSS
toc: true
author:
comments:
original:
permalink: 
image: https://www.7up.nl/images/mockup/product-single/lemonlemon/lemon-campaign-bg-mobile.jpg
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why

<!-- more -->

## logo
[七喜官网](https://www.7up.nl/7up, '动画效果很赞')
使用SVG作为背景，可以很好的应用了？

<a href="/7up" class="logo" id="logo">
	<span class="hidden">7UP</span>
</a>
<style type="text/css">
	.logo {
		position: absolute;
		top: 0;
		left: 0;
		width: 70px;
		height: 70px;
		cursor: pointer;
		background-image: url("https://www.7up.nl/images/design/logo.svg");
		background-size: 60px 60px;
		background-position: 100% 100%;
		background-repeat: no-repeat;
		z-index: 5
	}
	.hidden{
		visibility: hidden;
	}
	body:not(.isMobile) .logo:hover, body:not(.isMobile) .logo:focus, body:not(.isMobile) .logo:active {
		-webkit-animation: plopping 0.8s forwards;
		animation: plopping 0.8s forwards
	}
	@keyframes plopping {
		0% {
			-webkit-transform: scale(1);
			transform: scale(1)
		}

		20% {
			-webkit-transform: scale(0.85);
			transform: scale(0.85)
		}

		35% {
			-webkit-transform: scale(1.15);
			transform: scale(1.15)
		}

		50% {
			-webkit-transform: scale(0.9);
			transform: scale(0.9)
		}

		100% {
			-webkit-transform: scale(1);
			transform: scale(1)
		}
	
</style>


visibility: hidden;元素隐藏起来

拓展

> visibility=hidden, opacity=0，display:none
opacity=0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的。

visibility=hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件。

display=none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样。



### SVG
[TweenMax.js](https://www.tweenmax.com.cn/, '适用于移动端和现代互联网的超高性能专业级动画插件')


<style type="text/css">
	.side_navigation {
		position: absolute;
		right: 0;
		top: 50%;
		-webkit-transform: translateY(-50%);
		transform: translateY(-50%)
	}

	.navigation_list {
		position: relative;
		display: none;
		padding-left: 0;
		list-style-type: none
	}

	.side_navigation_item {
		position: relative;
		display: block;
		padding: 0.8rem 1.2rem;
		list-style-type: none;
		cursor: pointer
	}

	.side_navigation_item.return {
		margin-bottom: 1rem
	}

	body.isMobile 
	.side_navigation_item {
		padding: 1.5rem 0.8rem
	}

	body.isMobile 
	.side_navigation_item.return {
		margin-bottom: 2rem
	}
	.item_anchor {
		position: absolute;
		top: 0;
		bottom: 0;
		right: 47px;
		padding-right: 10px;
		padding-left: 20px;
		display: -webkit-flex;
		display: flex;
		-webkit-align-items: center;
		align-items: center;
		font-family: 'bentonsanscomp_lightregular', sans-serif;
		font-weight: normal;
		font-style: normal;
		white-space: nowrap;
		-webkit-transform: translateX(200px);
		transform: translateX(200px);
		will-change: color, transform, padding-right;
		transition: color 0.3s linear,padding-right 0.4s cubic-bezier(0.785, -0.565, 0.245, 1.64);
		-webkit-user-select: none !important
	}

	body.isMobile .item_anchor {
		right: 37px
	}

	.side_navigation_item.is_current .item_anchor {
		font-family: 'bentonsanscompbold', sans-serif;
		font-weight: normal;
		font-style: normal
	}

	.side_navigation_item.is_focused .item_anchor,
	.side_navigation_item.is_focused.is_current .item_anchor {
		padding-right: 23px;
		color: #00ab51;
		font-size: 1.1rem;
		font-family: 'bentonsanscompbold', sans-serif;
		font-weight: normal;
		font-style: normal
	}

	.item_arrow {
		position: relative;
		display: block;
		width: 13px;
		height: 13px
	}

	.item_arrow .nav_arrow {
		position: absolute;
		top: 2px;
		left: 0;
		width: 100%;
		height: auto
	}

	.item_arrow .arrow_path {
		stroke: #fff;
		stroke-width: 2;
		stroke-linejoin: round;
		stroke-linecap: round;
		fill: none
	}

	.navigation_list.is_open .arrow_path {
		stroke: #00ab51
	}

	.item_dot {
		display: block;
		position: relative;
		width: 10px;
		height: 10px;
		box-shadow: inset 0 0 0 2px #fff;
		border-radius: 50%;
		transition: box-shadow 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78)
	}

	.item_dot:before {
		content: '';
		position: absolute;
		top: calc(-300% + 5px);
		left: calc(-300% + 5px);
		width: 600%;
		height: 600%;
		border-radius: 50%;
		background-color: #00ab51;
		opacity: 0.6;
		will-change: transform, opacity;
		-webkit-transform: scale(0);
		transform: scale(0)
	}

	.side_navigation_item.is_current .item_dot {
		box-shadow: inset 0 0 0 6px #fff
	}

	.navigation_list.is_open 
	.side_navigation_item .item_dot {
		box-shadow: inset 0 0 0 2px #00ab51
	}

	.navigation_list.is_open 
	.side_navigation_item.is_current .item_dot {
		box-shadow: inset 0 0 0 6px #00ab51
	}

	.navigation_list.is_open 
	.side_navigation_item.is_focused .item_dot:before {
		-webkit-animation: pulse_dot 1s infinite cubic-bezier(0.85, 0.21, 0.165, 0.78);
		animation: pulse_dot 1s infinite cubic-bezier(0.85, 0.21, 0.165, 0.78)
	}

	@-webkit-keyframes pulse_dot {
		100% {
			-webkit-transform: scale(1);
			transform: scale(1);
			opacity: 0
		}
	}

	@keyframes pulse_dot {
		100% {
			-webkit-transform: scale(1);
			transform: scale(1);
			opacity: 0
		}
	}

	.side_navigation_media {
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		height: 100%
	}

	.side_navigation_media 
	.side_navigation_hitarea {
		position: absolute;
		top: 50%;
		right: 0;
		width: auto;
		height: 0;
		opacity: 0;
		-webkit-transform: translateY(-50%);
		transform: translateY(-50%)
	}

	.side_navigation_media 
	.side_navigation_hitarea path {
		fill: #0f0
	}

	.is_active 
	.side_navigation_media 
	.side_navigation_hitarea {
		height: 180%
	}

	.side_shape_front,.side_shape_back {
		position: absolute;
		top: 50%;
		right: 0;
		display: block;
		width: auto;
		-webkit-transform: translateY(-50%);
		transform: translateY(-50%);
		transition: height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),-webkit-transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78);
		transition: height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78);
		transition: height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),-webkit-transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78);
		pointer-events: none
	}

	.side_shape_front path,.side_shape_back path {
		display: none
	}

	.side_shape_back .side_shape_back_3,.side_shape_front .side_shape_front_1 {
		display: block
	}

	body.isMobile .side_shape_back .side_shape_back_3 {
		display: none
	}

	body.isMobile .side_shape_back .side_shape_back_1 {
		display: block
	}

	.side_shape_front path {
		fill: #fff
	}

	.side_shape_back path {
		fill: #00ab51
	}

	.side_shape_front {
		height: 270%
	}

	body.isMobile .side_shape_front {
		height: 180%
	}

	.side_shape_back {
		height: 270%
	}

	body.isMobile 
	.side_navigation.is_active .side_shape_back {
		height: 245%
	}

	.side_navigation.is_active .side_shape_back {
		height: 360%;
		-webkit-transform: translateY(-49%);
		transform: translateY(-49%)
	}

	body.isEdge .side_shape_front {
		position: absolute
	}

	body.isEdge .side_shape_back {
		position: relative;
		display: block;
		left: 100%;
		-webkit-transform: translateX(-100%) translateY(-50%);
		transform: translateX(-100%) translateY(-50%)
	}

	body.isEdge 
	.side_navigation.is_active .side_shape_back {
		-webkit-transform: translateX(-100%) translateY(-49%);
		transform: translateX(-100%) translateY(-49%)
	}

	body.isIE11 .side_shape_front,body.isIE11 .side_shape_back {
		transition: width 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),-webkit-transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78);
		transition: width 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78);
		transition: width 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),height 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78),-webkit-transform 0.3s cubic-bezier(0.85, 0.21, 0.165, 0.78)
	}

	body.isIE11 .side_shape_back {
		width: 345px;
		height: 531px;
		-webkit-transform: translateY(-50%);
		transform: translateY(-50%)
	}

	body.isIE11 .side_shape_front {
		width: 307px;
		height: 473px;
		-webkit-transform: translateY(-50%);
		transform: translateY(-50%)
	}

	body.isIE11 
	.side_navigation.is_active .side_shape_back {
		width: 423px;
		height: 645px;
		-webkit-transform: translateY(-49%);
		transform: translateY(-49%)
	}

	body.isIE11 .item_anchor {
		display: block;
		line-height: 36px
	}

	.cookie_banner {
		position: fixed;
		right: 0;
		bottom: 0;
		left: 0;
		padding: 2rem;
		background-color: #1c2c2b;
		box-shadow: 0 0 20px 2px rgba(28,44,43,0.2)
	}
</style>
<style type="text/css">
	#preloader {
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		display: -webkit-flex;
		display: flex;
		-webkit-flex-direction: column;
		flex-direction: column;
		-webkit-justify-content: center;
		justify-content: center;
	}
	.preloader_inner {
		position: relative;
		margin: auto
	}
	body.isIE11 .preloader_inner {
		margin: 0
	}
	.preloader_animation {
		position: relative;
		width: 80px;
		height: 80px;
		margin: 0 auto
	}
	.preloader_animation:before {
		content: '';
		position: absolute;
		top: 8px;
		right: 8px;
		bottom: 8px;
		left: 8px;
		background-color: #00ab51;
		border-radius: 50%;
		z-index: 10;
		-webkit-transform: scale(0);
		transform: scale(0);
		-webkit-animation: popup 0.6s 0.3s cubic-bezier(0.24, 1.65, 0.425, 0.92) forwards;
		animation: popup 0.6s 0.3s cubic-bezier(0.24, 1.65, 0.425, 0.92) forwards
	}
	@-webkit-keyframes popup {
		100% {
			-webkit-transform: scale(1);
			transform: scale(1)
		}
	}
	@keyframes popup {
		100% {
			-webkit-transform: scale(1);
			transform: scale(1)
		}
	}
	.preloader_circle {
		position: absolute;
		top: 0;
		left: 0;
		width: 80px;
		height: 80px;
		z-index: 0
	}
	.preloader_path {
		fill: none;
		stroke: #00ab51;
		stroke-linecap: round;
		stroke-miterlimit: 10;
		stroke-width: 3;
		display: none
	}
	.preloader_bubble {
		position: absolute;
		top: 8px;
		right: 8px;
		bottom: 8px;
		left: 8px;
		background-color: #00ab51;
		border-radius: 50%;
		-webkit-transform: scale(0);
		transform: scale(0);
		-webkit-animation: popup 0.6s 0.3s cubic-bezier(0.24, 1.65, 0.425, 0.92) forwards;
		animation: popup 0.6s 0.3s cubic-bezier(0.24, 1.65, 0.425, 0.92) forwards
	}
	.preloader_bubble:nth-child(2) {
		background-color: #fd0
	}
	.preloader_bubble:nth-child(4) {
		background-color: #82bc00
	}
	.preloader_bubble:nth-child(6) {
		background-color: #fd0
	}
	body.isIE11 .preloader_bubble {
		top: 10px;
		left: 10px;
		width: 60px;
		height: 60px
	}
	.preloader_bubble:nth-child(2) {
		width: 12px;
		height: 12px;
		-webkit-animation-name: loader_1;
		animation-name: loader_1;
		-webkit-animation-duration: 2.2s;
		animation-duration: 2.2s;
		-webkit-animation-delay: 0s;
		animation-delay: 0s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(3) {
		width: 20px;
		height: 20px;
		-webkit-animation-name: loader_2;
		animation-name: loader_2;
		-webkit-animation-duration: 2.9s;
		animation-duration: 2.9s;
		-webkit-animation-delay: .5s;
		animation-delay: .5s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(4) {
		width: 79px;
		height: 79px;
		-webkit-animation-name: loader_3;
		animation-name: loader_3;
		-webkit-animation-duration: 2.4s;
		animation-duration: 2.4s;
		-webkit-animation-delay: 1s;
		animation-delay: 1s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(5) {
		width: 7px;
		height: 7px;
		-webkit-animation-name: loader_4;
		animation-name: loader_4;
		-webkit-animation-duration: 2.9s;
		animation-duration: 2.9s;
		-webkit-animation-delay: 1.5s;
		animation-delay: 1.5s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(6) {
		width: 44px;
		height: 44px;
		-webkit-animation-name: loader_5;
		animation-name: loader_5;
		-webkit-animation-duration: 2.6s;
		animation-duration: 2.6s;
		-webkit-animation-delay: 2s;
		animation-delay: 2s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(7) {
		width: 48px;
		height: 48px;
		-webkit-animation-name: loader_6;
		animation-name: loader_6;
		-webkit-animation-duration: 2.4s;
		animation-duration: 2.4s;
		-webkit-animation-delay: 2.5s;
		animation-delay: 2.5s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(8) {
		width: 74px;
		height: 74px;
		-webkit-animation-name: loader_7;
		animation-name: loader_7;
		-webkit-animation-duration: 2.4s;
		animation-duration: 2.4s;
		-webkit-animation-delay: 3s;
		animation-delay: 3s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	.preloader_bubble:nth-child(9) {
		width: 57px;
		height: 57px;
		-webkit-animation-name: loader_8;
		animation-name: loader_8;
		-webkit-animation-duration: 2.5s;
		animation-duration: 2.5s;
		-webkit-animation-delay: 3.5s;
		animation-delay: 3.5s;
		-webkit-animation-iteration-count: infinite;
		animation-iteration-count: infinite;
		-webkit-animation-timing-function: linear;
		animation-timing-function: linear;
		-webkit-animation-play-state: running;
		animation-play-state: running
	}
	@-webkit-keyframes loader_1 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-5px) scale(.01);
			transform: translateX(3.99334px) translateY(-5px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-10px) scale(.02);
			transform: translateX(7.94677px) translateY(-10px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-15px) scale(.03);
			transform: translateX(11.82081px) translateY(-15px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-20px) scale(.04);
			transform: translateX(15.57673px) translateY(-20px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-25px) scale(.05);
			transform: translateX(19.17702px) translateY(-25px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-30px) scale(.06);
			transform: translateX(22.5857px) translateY(-30px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-35px) scale(.07);
			transform: translateX(25.76871px) translateY(-35px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-40px) scale(.08);
			transform: translateX(28.69424px) translateY(-40px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-45px) scale(.09);
			transform: translateX(31.33308px) translateY(-45px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-50px) scale(.1);
			transform: translateX(33.65884px) translateY(-50px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-55px) scale(.11);
			transform: translateX(35.64829px) translateY(-55px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-60px) scale(.12);
			transform: translateX(37.28156px) translateY(-60px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-65px) scale(.13);
			transform: translateX(38.54233px) translateY(-65px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-70px) scale(.14);
			transform: translateX(39.41799px) translateY(-70px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-75px) scale(.15);
			transform: translateX(39.8998px) translateY(-75px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-80px) scale(.16);
			transform: translateX(39.98294px) translateY(-80px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-85px) scale(.17);
			transform: translateX(39.66659px) translateY(-85px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-90px) scale(.18);
			transform: translateX(38.95391px) translateY(-90px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-95px) scale(.19);
			transform: translateX(37.852px) translateY(-95px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-100px) scale(.2);
			transform: translateX(36.3719px) translateY(-100px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-105px) scale(.21);
			transform: translateX(34.52837px) translateY(-105px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-110px) scale(.22);
			transform: translateX(32.33986px) translateY(-110px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-115px) scale(.23);
			transform: translateX(29.82821px) translateY(-115px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-120px) scale(.24);
			transform: translateX(27.01853px) translateY(-120px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-125px) scale(.25);
			transform: translateX(23.93889px) translateY(-125px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-130px) scale(.26);
			transform: translateX(20.62005px) translateY(-130px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-135px) scale(.27);
			transform: translateX(17.0952px) translateY(-135px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-140px) scale(.28);
			transform: translateX(13.39953px) translateY(-140px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-145px) scale(.29);
			transform: translateX(9.56997px) translateY(-145px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-150px) scale(.3);
			transform: translateX(5.6448px) translateY(-150px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-155px) scale(.31);
			transform: translateX(1.66323px) translateY(-155px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-160px) scale(.32);
			transform: translateX(-2.33497px) translateY(-160px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-165px) scale(.33);
			transform: translateX(-6.30983px) translateY(-165px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-170px) scale(.34);
			transform: translateX(-10.22164px) translateY(-170px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-175px) scale(.35);
			transform: translateX(-14.03133px) translateY(-175px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-180px) scale(.36);
			transform: translateX(-17.70082px) translateY(-180px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-185px) scale(.37);
			transform: translateX(-21.19345px) translateY(-185px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-190px) scale(.38);
			transform: translateX(-24.47432px) translateY(-190px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-195px) scale(.39);
			transform: translateX(-27.51065px) translateY(-195px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-200px) scale(.4);
			transform: translateX(-30.2721px) translateY(-200px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-205px) scale(.41);
			transform: translateX(-32.73108px) translateY(-205px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-210px) scale(.42);
			transform: translateX(-34.86303px) translateY(-210px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-215px) scale(.43);
			transform: translateX(-36.64664px) translateY(-215px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-220px) scale(.44);
			transform: translateX(-38.06408px) translateY(-220px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-225px) scale(.45);
			transform: translateX(-39.1012px) translateY(-225px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-230px) scale(.46);
			transform: translateX(-39.74764px) translateY(-230px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-235px) scale(.47);
			transform: translateX(-39.99693px) translateY(-235px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-240px) scale(.48);
			transform: translateX(-39.84658px) translateY(-240px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-245px) scale(.49);
			transform: translateX(-39.29809px) translateY(-245px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-250px) scale(.5);
			transform: translateX(-38.35695px) translateY(-250px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-255px) scale(.49);
			transform: translateX(-37.03256px) translateY(-255px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-260px) scale(.48);
			transform: translateX(-35.33814px) translateY(-260px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-265px) scale(.47);
			transform: translateX(-33.29063px) translateY(-265px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-270px) scale(.46);
			transform: translateX(-30.91048px) translateY(-270px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-275px) scale(.45);
			transform: translateX(-28.22146px) translateY(-275px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-280px) scale(.44);
			transform: translateX(-25.25043px) translateY(-280px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-285px) scale(.43);
			transform: translateX(-22.02707px) translateY(-285px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-290px) scale(.42);
			transform: translateX(-18.58356px) translateY(-290px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-295px) scale(.41);
			transform: translateX(-14.95428px) translateY(-295px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-300px) scale(.4);
			transform: translateX(-11.17547px) translateY(-300px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-305px) scale(.39);
			transform: translateX(-7.28482px) translateY(-305px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-310px) scale(.38);
			transform: translateX(-3.32114px) translateY(-310px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-315px) scale(.37);
			transform: translateX(.67607px) translateY(-315px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-320px) scale(.36);
			transform: translateX(4.66701px) translateY(-320px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-325px) scale(.35);
			transform: translateX(8.61199px) translateY(-325px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-330px) scale(.34);
			transform: translateX(12.47185px) translateY(-330px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-335px) scale(.33);
			transform: translateX(16.20837px) translateY(-335px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-340px) scale(.32);
			transform: translateX(19.7847px) translateY(-340px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-345px) scale(.31);
			transform: translateX(23.16575px) translateY(-345px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-350px) scale(.3);
			transform: translateX(26.31858px) translateY(-350px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-355px) scale(.29);
			transform: translateX(29.21285px) translateY(-355px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-360px) scale(.28);
			transform: translateX(31.82116px) translateY(-360px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-365px) scale(.27);
			transform: translateX(34.11946px) translateY(-365px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-370px) scale(.26);
			transform: translateX(36.08748px) translateY(-370px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-375px) scale(.25);
			transform: translateX(37.70905px) translateY(-375px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-380px) scale(.24);
			transform: translateX(38.97256px) translateY(-380px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-385px) scale(.23);
			transform: translateX(39.87139px) translateY(-385px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-390px) scale(.22);
			transform: translateX(40.40437px) translateY(-390px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-395px) scale(.21);
			transform: translateX(40.57628px) translateY(-395px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-400px) scale(.2);
			transform: translateX(40.39848px) translateY(-400px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-405px) scale(.19);
			transform: translateX(39.88958px) translateY(-405px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-410px) scale(.18);
			transform: translateX(39.07627px) translateY(-410px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-415px) scale(.17);
			transform: translateX(37.99434px) translateY(-415px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-420px) scale(.16);
			transform: translateX(36.68989px) translateY(-420px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-425px) scale(.15);
			transform: translateX(35.22086px) translateY(-425px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-430px) scale(.14);
			transform: translateX(33.65889px) translateY(-430px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-435px) scale(.13);
			transform: translateX(32.09164px) translateY(-435px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-440px) scale(.12);
			transform: translateX(30.62571px) translateY(-440px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-445px) scale(.11);
			transform: translateX(29.39012px) translateY(-445px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-450px) scale(.1);
			transform: translateX(28.54081px) translateY(-450px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-455px) scale(.09);
			transform: translateX(28.26597px) translateY(-455px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-460px) scale(.08);
			transform: translateX(28.79279px) translateY(-460px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-465px) scale(.07);
			transform: translateX(30.39554px) translateY(-465px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-470px) scale(.06);
			transform: translateX(33.4056px) translateY(-470px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-475px) scale(.05);
			transform: translateX(38.22359px) translateY(-475px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-480px) scale(.04);
			transform: translateX(45.3341px) translateY(-480px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-485px) scale(.03);
			transform: translateX(55.3236px) translateY(-485px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-490px) scale(.02);
			transform: translateX(68.90201px) translateY(-490px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-495px) scale(.01);
			transform: translateX(86.92866px) translateY(-495px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-500px) scale(0);
			transform: translateX(110.44364px) translateY(-500px) scale(0)
		}	}
	@keyframes loader_1 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-5px) scale(.01);
			transform: translateX(3.99334px) translateY(-5px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-10px) scale(.02);
			transform: translateX(7.94677px) translateY(-10px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-15px) scale(.03);
			transform: translateX(11.82081px) translateY(-15px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-20px) scale(.04);
			transform: translateX(15.57673px) translateY(-20px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-25px) scale(.05);
			transform: translateX(19.17702px) translateY(-25px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-30px) scale(.06);
			transform: translateX(22.5857px) translateY(-30px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-35px) scale(.07);
			transform: translateX(25.76871px) translateY(-35px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-40px) scale(.08);
			transform: translateX(28.69424px) translateY(-40px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-45px) scale(.09);
			transform: translateX(31.33308px) translateY(-45px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-50px) scale(.1);
			transform: translateX(33.65884px) translateY(-50px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-55px) scale(.11);
			transform: translateX(35.64829px) translateY(-55px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-60px) scale(.12);
			transform: translateX(37.28156px) translateY(-60px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-65px) scale(.13);
			transform: translateX(38.54233px) translateY(-65px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-70px) scale(.14);
			transform: translateX(39.41799px) translateY(-70px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-75px) scale(.15);
			transform: translateX(39.8998px) translateY(-75px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-80px) scale(.16);
			transform: translateX(39.98294px) translateY(-80px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-85px) scale(.17);
			transform: translateX(39.66659px) translateY(-85px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-90px) scale(.18);
			transform: translateX(38.95391px) translateY(-90px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-95px) scale(.19);
			transform: translateX(37.852px) translateY(-95px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-100px) scale(.2);
			transform: translateX(36.3719px) translateY(-100px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-105px) scale(.21);
			transform: translateX(34.52837px) translateY(-105px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-110px) scale(.22);
			transform: translateX(32.33986px) translateY(-110px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-115px) scale(.23);
			transform: translateX(29.82821px) translateY(-115px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-120px) scale(.24);
			transform: translateX(27.01853px) translateY(-120px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-125px) scale(.25);
			transform: translateX(23.93889px) translateY(-125px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-130px) scale(.26);
			transform: translateX(20.62005px) translateY(-130px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-135px) scale(.27);
			transform: translateX(17.0952px) translateY(-135px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-140px) scale(.28);
			transform: translateX(13.39953px) translateY(-140px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-145px) scale(.29);
			transform: translateX(9.56997px) translateY(-145px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-150px) scale(.3);
			transform: translateX(5.6448px) translateY(-150px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-155px) scale(.31);
			transform: translateX(1.66323px) translateY(-155px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-160px) scale(.32);
			transform: translateX(-2.33497px) translateY(-160px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-165px) scale(.33);
			transform: translateX(-6.30983px) translateY(-165px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-170px) scale(.34);
			transform: translateX(-10.22164px) translateY(-170px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-175px) scale(.35);
			transform: translateX(-14.03133px) translateY(-175px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-180px) scale(.36);
			transform: translateX(-17.70082px) translateY(-180px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-185px) scale(.37);
			transform: translateX(-21.19345px) translateY(-185px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-190px) scale(.38);
			transform: translateX(-24.47432px) translateY(-190px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-195px) scale(.39);
			transform: translateX(-27.51065px) translateY(-195px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-200px) scale(.4);
			transform: translateX(-30.2721px) translateY(-200px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-205px) scale(.41);
			transform: translateX(-32.73108px) translateY(-205px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-210px) scale(.42);
			transform: translateX(-34.86303px) translateY(-210px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-215px) scale(.43);
			transform: translateX(-36.64664px) translateY(-215px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-220px) scale(.44);
			transform: translateX(-38.06408px) translateY(-220px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-225px) scale(.45);
			transform: translateX(-39.1012px) translateY(-225px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-230px) scale(.46);
			transform: translateX(-39.74764px) translateY(-230px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-235px) scale(.47);
			transform: translateX(-39.99693px) translateY(-235px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-240px) scale(.48);
			transform: translateX(-39.84658px) translateY(-240px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-245px) scale(.49);
			transform: translateX(-39.29809px) translateY(-245px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-250px) scale(.5);
			transform: translateX(-38.35695px) translateY(-250px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-255px) scale(.49);
			transform: translateX(-37.03256px) translateY(-255px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-260px) scale(.48);
			transform: translateX(-35.33814px) translateY(-260px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-265px) scale(.47);
			transform: translateX(-33.29063px) translateY(-265px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-270px) scale(.46);
			transform: translateX(-30.91048px) translateY(-270px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-275px) scale(.45);
			transform: translateX(-28.22146px) translateY(-275px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-280px) scale(.44);
			transform: translateX(-25.25043px) translateY(-280px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-285px) scale(.43);
			transform: translateX(-22.02707px) translateY(-285px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-290px) scale(.42);
			transform: translateX(-18.58356px) translateY(-290px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-295px) scale(.41);
			transform: translateX(-14.95428px) translateY(-295px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-300px) scale(.4);
			transform: translateX(-11.17547px) translateY(-300px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-305px) scale(.39);
			transform: translateX(-7.28482px) translateY(-305px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-310px) scale(.38);
			transform: translateX(-3.32114px) translateY(-310px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-315px) scale(.37);
			transform: translateX(.67607px) translateY(-315px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-320px) scale(.36);
			transform: translateX(4.66701px) translateY(-320px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-325px) scale(.35);
			transform: translateX(8.61199px) translateY(-325px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-330px) scale(.34);
			transform: translateX(12.47185px) translateY(-330px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-335px) scale(.33);
			transform: translateX(16.20837px) translateY(-335px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-340px) scale(.32);
			transform: translateX(19.7847px) translateY(-340px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-345px) scale(.31);
			transform: translateX(23.16575px) translateY(-345px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-350px) scale(.3);
			transform: translateX(26.31858px) translateY(-350px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-355px) scale(.29);
			transform: translateX(29.21285px) translateY(-355px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-360px) scale(.28);
			transform: translateX(31.82116px) translateY(-360px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-365px) scale(.27);
			transform: translateX(34.11946px) translateY(-365px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-370px) scale(.26);
			transform: translateX(36.08748px) translateY(-370px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-375px) scale(.25);
			transform: translateX(37.70905px) translateY(-375px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-380px) scale(.24);
			transform: translateX(38.97256px) translateY(-380px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-385px) scale(.23);
			transform: translateX(39.87139px) translateY(-385px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-390px) scale(.22);
			transform: translateX(40.40437px) translateY(-390px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-395px) scale(.21);
			transform: translateX(40.57628px) translateY(-395px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-400px) scale(.2);
			transform: translateX(40.39848px) translateY(-400px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-405px) scale(.19);
			transform: translateX(39.88958px) translateY(-405px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-410px) scale(.18);
			transform: translateX(39.07627px) translateY(-410px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-415px) scale(.17);
			transform: translateX(37.99434px) translateY(-415px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-420px) scale(.16);
			transform: translateX(36.68989px) translateY(-420px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-425px) scale(.15);
			transform: translateX(35.22086px) translateY(-425px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-430px) scale(.14);
			transform: translateX(33.65889px) translateY(-430px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-435px) scale(.13);
			transform: translateX(32.09164px) translateY(-435px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-440px) scale(.12);
			transform: translateX(30.62571px) translateY(-440px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-445px) scale(.11);
			transform: translateX(29.39012px) translateY(-445px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-450px) scale(.1);
			transform: translateX(28.54081px) translateY(-450px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-455px) scale(.09);
			transform: translateX(28.26597px) translateY(-455px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-460px) scale(.08);
			transform: translateX(28.79279px) translateY(-460px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-465px) scale(.07);
			transform: translateX(30.39554px) translateY(-465px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-470px) scale(.06);
			transform: translateX(33.4056px) translateY(-470px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-475px) scale(.05);
			transform: translateX(38.22359px) translateY(-475px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-480px) scale(.04);
			transform: translateX(45.3341px) translateY(-480px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-485px) scale(.03);
			transform: translateX(55.3236px) translateY(-485px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-490px) scale(.02);
			transform: translateX(68.90201px) translateY(-490px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-495px) scale(.01);
			transform: translateX(86.92866px) translateY(-495px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-500px) scale(0);
			transform: translateX(110.44364px) translateY(-500px) scale(0)
		}	}
	@-webkit-keyframes loader_2 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@keyframes loader_2 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@-webkit-keyframes loader_3 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-4px) scale(.01);
			transform: translateX(3.99334px) translateY(-4px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-8px) scale(.02);
			transform: translateX(7.94677px) translateY(-8px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-12px) scale(.03);
			transform: translateX(11.82081px) translateY(-12px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-16px) scale(.04);
			transform: translateX(15.57673px) translateY(-16px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-20px) scale(.05);
			transform: translateX(19.17702px) translateY(-20px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-24px) scale(.06);
			transform: translateX(22.5857px) translateY(-24px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-28px) scale(.07);
			transform: translateX(25.76871px) translateY(-28px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-32px) scale(.08);
			transform: translateX(28.69424px) translateY(-32px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-36px) scale(.09);
			transform: translateX(31.33308px) translateY(-36px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-40px) scale(.1);
			transform: translateX(33.65884px) translateY(-40px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-44px) scale(.11);
			transform: translateX(35.64829px) translateY(-44px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-48px) scale(.12);
			transform: translateX(37.28156px) translateY(-48px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-52px) scale(.13);
			transform: translateX(38.54233px) translateY(-52px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-56px) scale(.14);
			transform: translateX(39.41799px) translateY(-56px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-60px) scale(.15);
			transform: translateX(39.8998px) translateY(-60px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-64px) scale(.16);
			transform: translateX(39.98294px) translateY(-64px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-68px) scale(.17);
			transform: translateX(39.66659px) translateY(-68px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-72px) scale(.18);
			transform: translateX(38.95391px) translateY(-72px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-76px) scale(.19);
			transform: translateX(37.852px) translateY(-76px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-80px) scale(.2);
			transform: translateX(36.3719px) translateY(-80px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-84px) scale(.21);
			transform: translateX(34.52837px) translateY(-84px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-88px) scale(.22);
			transform: translateX(32.33986px) translateY(-88px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-92px) scale(.23);
			transform: translateX(29.82821px) translateY(-92px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-96px) scale(.24);
			transform: translateX(27.01853px) translateY(-96px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-100px) scale(.25);
			transform: translateX(23.93889px) translateY(-100px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-104px) scale(.26);
			transform: translateX(20.62005px) translateY(-104px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-108px) scale(.27);
			transform: translateX(17.0952px) translateY(-108px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-112px) scale(.28);
			transform: translateX(13.39953px) translateY(-112px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-116px) scale(.29);
			transform: translateX(9.56997px) translateY(-116px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-120px) scale(.3);
			transform: translateX(5.6448px) translateY(-120px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-124px) scale(.31);
			transform: translateX(1.66323px) translateY(-124px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-128px) scale(.32);
			transform: translateX(-2.33497px) translateY(-128px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-132px) scale(.33);
			transform: translateX(-6.30983px) translateY(-132px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-136px) scale(.34);
			transform: translateX(-10.22164px) translateY(-136px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-140px) scale(.35);
			transform: translateX(-14.03133px) translateY(-140px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-144px) scale(.36);
			transform: translateX(-17.70082px) translateY(-144px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-148px) scale(.37);
			transform: translateX(-21.19345px) translateY(-148px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-152px) scale(.38);
			transform: translateX(-24.47432px) translateY(-152px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-156px) scale(.39);
			transform: translateX(-27.51065px) translateY(-156px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-160px) scale(.4);
			transform: translateX(-30.2721px) translateY(-160px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-164px) scale(.41);
			transform: translateX(-32.73108px) translateY(-164px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-168px) scale(.42);
			transform: translateX(-34.86303px) translateY(-168px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-172px) scale(.43);
			transform: translateX(-36.64664px) translateY(-172px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-176px) scale(.44);
			transform: translateX(-38.06408px) translateY(-176px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-180px) scale(.45);
			transform: translateX(-39.1012px) translateY(-180px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-184px) scale(.46);
			transform: translateX(-39.74764px) translateY(-184px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-188px) scale(.47);
			transform: translateX(-39.99693px) translateY(-188px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-192px) scale(.48);
			transform: translateX(-39.84658px) translateY(-192px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-196px) scale(.49);
			transform: translateX(-39.29809px) translateY(-196px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-200px) scale(.5);
			transform: translateX(-38.35695px) translateY(-200px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-204px) scale(.49);
			transform: translateX(-37.03256px) translateY(-204px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-208px) scale(.48);
			transform: translateX(-35.33814px) translateY(-208px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-212px) scale(.47);
			transform: translateX(-33.29063px) translateY(-212px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-216px) scale(.46);
			transform: translateX(-30.91048px) translateY(-216px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-220px) scale(.45);
			transform: translateX(-28.22146px) translateY(-220px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-224px) scale(.44);
			transform: translateX(-25.25043px) translateY(-224px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-228px) scale(.43);
			transform: translateX(-22.02707px) translateY(-228px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-232px) scale(.42);
			transform: translateX(-18.58356px) translateY(-232px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-236px) scale(.41);
			transform: translateX(-14.95428px) translateY(-236px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-240px) scale(.4);
			transform: translateX(-11.17547px) translateY(-240px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-244px) scale(.39);
			transform: translateX(-7.28482px) translateY(-244px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-248px) scale(.38);
			transform: translateX(-3.32114px) translateY(-248px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-252px) scale(.37);
			transform: translateX(.67607px) translateY(-252px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-256px) scale(.36);
			transform: translateX(4.66701px) translateY(-256px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-260px) scale(.35);
			transform: translateX(8.61199px) translateY(-260px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-264px) scale(.34);
			transform: translateX(12.47185px) translateY(-264px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-268px) scale(.33);
			transform: translateX(16.20837px) translateY(-268px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-272px) scale(.32);
			transform: translateX(19.7847px) translateY(-272px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-276px) scale(.31);
			transform: translateX(23.16575px) translateY(-276px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-280px) scale(.3);
			transform: translateX(26.31858px) translateY(-280px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-284px) scale(.29);
			transform: translateX(29.21285px) translateY(-284px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-288px) scale(.28);
			transform: translateX(31.82116px) translateY(-288px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-292px) scale(.27);
			transform: translateX(34.11946px) translateY(-292px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-296px) scale(.26);
			transform: translateX(36.08748px) translateY(-296px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-300px) scale(.25);
			transform: translateX(37.70905px) translateY(-300px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-304px) scale(.24);
			transform: translateX(38.97256px) translateY(-304px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-308px) scale(.23);
			transform: translateX(39.87139px) translateY(-308px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-312px) scale(.22);
			transform: translateX(40.40437px) translateY(-312px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-316px) scale(.21);
			transform: translateX(40.57628px) translateY(-316px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-320px) scale(.2);
			transform: translateX(40.39848px) translateY(-320px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-324px) scale(.19);
			transform: translateX(39.88958px) translateY(-324px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-328px) scale(.18);
			transform: translateX(39.07627px) translateY(-328px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-332px) scale(.17);
			transform: translateX(37.99434px) translateY(-332px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-336px) scale(.16);
			transform: translateX(36.68989px) translateY(-336px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-340px) scale(.15);
			transform: translateX(35.22086px) translateY(-340px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-344px) scale(.14);
			transform: translateX(33.65889px) translateY(-344px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-348px) scale(.13);
			transform: translateX(32.09164px) translateY(-348px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-352px) scale(.12);
			transform: translateX(30.62571px) translateY(-352px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-356px) scale(.11);
			transform: translateX(29.39012px) translateY(-356px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-360px) scale(.1);
			transform: translateX(28.54081px) translateY(-360px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-364px) scale(.09);
			transform: translateX(28.26597px) translateY(-364px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-368px) scale(.08);
			transform: translateX(28.79279px) translateY(-368px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-372px) scale(.07);
			transform: translateX(30.39554px) translateY(-372px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-376px) scale(.06);
			transform: translateX(33.4056px) translateY(-376px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-380px) scale(.05);
			transform: translateX(38.22359px) translateY(-380px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-384px) scale(.04);
			transform: translateX(45.3341px) translateY(-384px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-388px) scale(.03);
			transform: translateX(55.3236px) translateY(-388px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-392px) scale(.02);
			transform: translateX(68.90201px) translateY(-392px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-396px) scale(.01);
			transform: translateX(86.92866px) translateY(-396px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-400px) scale(0);
			transform: translateX(110.44364px) translateY(-400px) scale(0)
		}	}
	@keyframes loader_3 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-4px) scale(.01);
			transform: translateX(3.99334px) translateY(-4px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-8px) scale(.02);
			transform: translateX(7.94677px) translateY(-8px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-12px) scale(.03);
			transform: translateX(11.82081px) translateY(-12px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-16px) scale(.04);
			transform: translateX(15.57673px) translateY(-16px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-20px) scale(.05);
			transform: translateX(19.17702px) translateY(-20px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-24px) scale(.06);
			transform: translateX(22.5857px) translateY(-24px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-28px) scale(.07);
			transform: translateX(25.76871px) translateY(-28px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-32px) scale(.08);
			transform: translateX(28.69424px) translateY(-32px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-36px) scale(.09);
			transform: translateX(31.33308px) translateY(-36px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-40px) scale(.1);
			transform: translateX(33.65884px) translateY(-40px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-44px) scale(.11);
			transform: translateX(35.64829px) translateY(-44px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-48px) scale(.12);
			transform: translateX(37.28156px) translateY(-48px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-52px) scale(.13);
			transform: translateX(38.54233px) translateY(-52px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-56px) scale(.14);
			transform: translateX(39.41799px) translateY(-56px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-60px) scale(.15);
			transform: translateX(39.8998px) translateY(-60px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-64px) scale(.16);
			transform: translateX(39.98294px) translateY(-64px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-68px) scale(.17);
			transform: translateX(39.66659px) translateY(-68px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-72px) scale(.18);
			transform: translateX(38.95391px) translateY(-72px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-76px) scale(.19);
			transform: translateX(37.852px) translateY(-76px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-80px) scale(.2);
			transform: translateX(36.3719px) translateY(-80px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-84px) scale(.21);
			transform: translateX(34.52837px) translateY(-84px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-88px) scale(.22);
			transform: translateX(32.33986px) translateY(-88px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-92px) scale(.23);
			transform: translateX(29.82821px) translateY(-92px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-96px) scale(.24);
			transform: translateX(27.01853px) translateY(-96px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-100px) scale(.25);
			transform: translateX(23.93889px) translateY(-100px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-104px) scale(.26);
			transform: translateX(20.62005px) translateY(-104px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-108px) scale(.27);
			transform: translateX(17.0952px) translateY(-108px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-112px) scale(.28);
			transform: translateX(13.39953px) translateY(-112px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-116px) scale(.29);
			transform: translateX(9.56997px) translateY(-116px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-120px) scale(.3);
			transform: translateX(5.6448px) translateY(-120px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-124px) scale(.31);
			transform: translateX(1.66323px) translateY(-124px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-128px) scale(.32);
			transform: translateX(-2.33497px) translateY(-128px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-132px) scale(.33);
			transform: translateX(-6.30983px) translateY(-132px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-136px) scale(.34);
			transform: translateX(-10.22164px) translateY(-136px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-140px) scale(.35);
			transform: translateX(-14.03133px) translateY(-140px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-144px) scale(.36);
			transform: translateX(-17.70082px) translateY(-144px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-148px) scale(.37);
			transform: translateX(-21.19345px) translateY(-148px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-152px) scale(.38);
			transform: translateX(-24.47432px) translateY(-152px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-156px) scale(.39);
			transform: translateX(-27.51065px) translateY(-156px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-160px) scale(.4);
			transform: translateX(-30.2721px) translateY(-160px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-164px) scale(.41);
			transform: translateX(-32.73108px) translateY(-164px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-168px) scale(.42);
			transform: translateX(-34.86303px) translateY(-168px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-172px) scale(.43);
			transform: translateX(-36.64664px) translateY(-172px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-176px) scale(.44);
			transform: translateX(-38.06408px) translateY(-176px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-180px) scale(.45);
			transform: translateX(-39.1012px) translateY(-180px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-184px) scale(.46);
			transform: translateX(-39.74764px) translateY(-184px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-188px) scale(.47);
			transform: translateX(-39.99693px) translateY(-188px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-192px) scale(.48);
			transform: translateX(-39.84658px) translateY(-192px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-196px) scale(.49);
			transform: translateX(-39.29809px) translateY(-196px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-200px) scale(.5);
			transform: translateX(-38.35695px) translateY(-200px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-204px) scale(.49);
			transform: translateX(-37.03256px) translateY(-204px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-208px) scale(.48);
			transform: translateX(-35.33814px) translateY(-208px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-212px) scale(.47);
			transform: translateX(-33.29063px) translateY(-212px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-216px) scale(.46);
			transform: translateX(-30.91048px) translateY(-216px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-220px) scale(.45);
			transform: translateX(-28.22146px) translateY(-220px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-224px) scale(.44);
			transform: translateX(-25.25043px) translateY(-224px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-228px) scale(.43);
			transform: translateX(-22.02707px) translateY(-228px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-232px) scale(.42);
			transform: translateX(-18.58356px) translateY(-232px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-236px) scale(.41);
			transform: translateX(-14.95428px) translateY(-236px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-240px) scale(.4);
			transform: translateX(-11.17547px) translateY(-240px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-244px) scale(.39);
			transform: translateX(-7.28482px) translateY(-244px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-248px) scale(.38);
			transform: translateX(-3.32114px) translateY(-248px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-252px) scale(.37);
			transform: translateX(.67607px) translateY(-252px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-256px) scale(.36);
			transform: translateX(4.66701px) translateY(-256px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-260px) scale(.35);
			transform: translateX(8.61199px) translateY(-260px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-264px) scale(.34);
			transform: translateX(12.47185px) translateY(-264px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-268px) scale(.33);
			transform: translateX(16.20837px) translateY(-268px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-272px) scale(.32);
			transform: translateX(19.7847px) translateY(-272px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-276px) scale(.31);
			transform: translateX(23.16575px) translateY(-276px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-280px) scale(.3);
			transform: translateX(26.31858px) translateY(-280px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-284px) scale(.29);
			transform: translateX(29.21285px) translateY(-284px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-288px) scale(.28);
			transform: translateX(31.82116px) translateY(-288px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-292px) scale(.27);
			transform: translateX(34.11946px) translateY(-292px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-296px) scale(.26);
			transform: translateX(36.08748px) translateY(-296px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-300px) scale(.25);
			transform: translateX(37.70905px) translateY(-300px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-304px) scale(.24);
			transform: translateX(38.97256px) translateY(-304px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-308px) scale(.23);
			transform: translateX(39.87139px) translateY(-308px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-312px) scale(.22);
			transform: translateX(40.40437px) translateY(-312px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-316px) scale(.21);
			transform: translateX(40.57628px) translateY(-316px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-320px) scale(.2);
			transform: translateX(40.39848px) translateY(-320px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-324px) scale(.19);
			transform: translateX(39.88958px) translateY(-324px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-328px) scale(.18);
			transform: translateX(39.07627px) translateY(-328px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-332px) scale(.17);
			transform: translateX(37.99434px) translateY(-332px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-336px) scale(.16);
			transform: translateX(36.68989px) translateY(-336px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-340px) scale(.15);
			transform: translateX(35.22086px) translateY(-340px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-344px) scale(.14);
			transform: translateX(33.65889px) translateY(-344px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-348px) scale(.13);
			transform: translateX(32.09164px) translateY(-348px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-352px) scale(.12);
			transform: translateX(30.62571px) translateY(-352px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-356px) scale(.11);
			transform: translateX(29.39012px) translateY(-356px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-360px) scale(.1);
			transform: translateX(28.54081px) translateY(-360px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-364px) scale(.09);
			transform: translateX(28.26597px) translateY(-364px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-368px) scale(.08);
			transform: translateX(28.79279px) translateY(-368px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-372px) scale(.07);
			transform: translateX(30.39554px) translateY(-372px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-376px) scale(.06);
			transform: translateX(33.4056px) translateY(-376px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-380px) scale(.05);
			transform: translateX(38.22359px) translateY(-380px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-384px) scale(.04);
			transform: translateX(45.3341px) translateY(-384px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-388px) scale(.03);
			transform: translateX(55.3236px) translateY(-388px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-392px) scale(.02);
			transform: translateX(68.90201px) translateY(-392px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-396px) scale(.01);
			transform: translateX(86.92866px) translateY(-396px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-400px) scale(0);
			transform: translateX(110.44364px) translateY(-400px) scale(0)
		}	}
	@-webkit-keyframes loader_4 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-4px) scale(.01);
			transform: translateX(3.99334px) translateY(-4px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-8px) scale(.02);
			transform: translateX(7.94677px) translateY(-8px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-12px) scale(.03);
			transform: translateX(11.82081px) translateY(-12px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-16px) scale(.04);
			transform: translateX(15.57673px) translateY(-16px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-20px) scale(.05);
			transform: translateX(19.17702px) translateY(-20px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-24px) scale(.06);
			transform: translateX(22.5857px) translateY(-24px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-28px) scale(.07);
			transform: translateX(25.76871px) translateY(-28px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-32px) scale(.08);
			transform: translateX(28.69424px) translateY(-32px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-36px) scale(.09);
			transform: translateX(31.33308px) translateY(-36px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-40px) scale(.1);
			transform: translateX(33.65884px) translateY(-40px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-44px) scale(.11);
			transform: translateX(35.64829px) translateY(-44px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-48px) scale(.12);
			transform: translateX(37.28156px) translateY(-48px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-52px) scale(.13);
			transform: translateX(38.54233px) translateY(-52px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-56px) scale(.14);
			transform: translateX(39.41799px) translateY(-56px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-60px) scale(.15);
			transform: translateX(39.8998px) translateY(-60px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-64px) scale(.16);
			transform: translateX(39.98294px) translateY(-64px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-68px) scale(.17);
			transform: translateX(39.66659px) translateY(-68px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-72px) scale(.18);
			transform: translateX(38.95391px) translateY(-72px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-76px) scale(.19);
			transform: translateX(37.852px) translateY(-76px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-80px) scale(.2);
			transform: translateX(36.3719px) translateY(-80px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-84px) scale(.21);
			transform: translateX(34.52837px) translateY(-84px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-88px) scale(.22);
			transform: translateX(32.33986px) translateY(-88px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-92px) scale(.23);
			transform: translateX(29.82821px) translateY(-92px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-96px) scale(.24);
			transform: translateX(27.01853px) translateY(-96px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-100px) scale(.25);
			transform: translateX(23.93889px) translateY(-100px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-104px) scale(.26);
			transform: translateX(20.62005px) translateY(-104px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-108px) scale(.27);
			transform: translateX(17.0952px) translateY(-108px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-112px) scale(.28);
			transform: translateX(13.39953px) translateY(-112px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-116px) scale(.29);
			transform: translateX(9.56997px) translateY(-116px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-120px) scale(.3);
			transform: translateX(5.6448px) translateY(-120px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-124px) scale(.31);
			transform: translateX(1.66323px) translateY(-124px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-128px) scale(.32);
			transform: translateX(-2.33497px) translateY(-128px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-132px) scale(.33);
			transform: translateX(-6.30983px) translateY(-132px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-136px) scale(.34);
			transform: translateX(-10.22164px) translateY(-136px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-140px) scale(.35);
			transform: translateX(-14.03133px) translateY(-140px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-144px) scale(.36);
			transform: translateX(-17.70082px) translateY(-144px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-148px) scale(.37);
			transform: translateX(-21.19345px) translateY(-148px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-152px) scale(.38);
			transform: translateX(-24.47432px) translateY(-152px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-156px) scale(.39);
			transform: translateX(-27.51065px) translateY(-156px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-160px) scale(.4);
			transform: translateX(-30.2721px) translateY(-160px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-164px) scale(.41);
			transform: translateX(-32.73108px) translateY(-164px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-168px) scale(.42);
			transform: translateX(-34.86303px) translateY(-168px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-172px) scale(.43);
			transform: translateX(-36.64664px) translateY(-172px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-176px) scale(.44);
			transform: translateX(-38.06408px) translateY(-176px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-180px) scale(.45);
			transform: translateX(-39.1012px) translateY(-180px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-184px) scale(.46);
			transform: translateX(-39.74764px) translateY(-184px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-188px) scale(.47);
			transform: translateX(-39.99693px) translateY(-188px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-192px) scale(.48);
			transform: translateX(-39.84658px) translateY(-192px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-196px) scale(.49);
			transform: translateX(-39.29809px) translateY(-196px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-200px) scale(.5);
			transform: translateX(-38.35695px) translateY(-200px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-204px) scale(.49);
			transform: translateX(-37.03256px) translateY(-204px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-208px) scale(.48);
			transform: translateX(-35.33814px) translateY(-208px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-212px) scale(.47);
			transform: translateX(-33.29063px) translateY(-212px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-216px) scale(.46);
			transform: translateX(-30.91048px) translateY(-216px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-220px) scale(.45);
			transform: translateX(-28.22146px) translateY(-220px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-224px) scale(.44);
			transform: translateX(-25.25043px) translateY(-224px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-228px) scale(.43);
			transform: translateX(-22.02707px) translateY(-228px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-232px) scale(.42);
			transform: translateX(-18.58356px) translateY(-232px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-236px) scale(.41);
			transform: translateX(-14.95428px) translateY(-236px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-240px) scale(.4);
			transform: translateX(-11.17547px) translateY(-240px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-244px) scale(.39);
			transform: translateX(-7.28482px) translateY(-244px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-248px) scale(.38);
			transform: translateX(-3.32114px) translateY(-248px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-252px) scale(.37);
			transform: translateX(.67607px) translateY(-252px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-256px) scale(.36);
			transform: translateX(4.66701px) translateY(-256px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-260px) scale(.35);
			transform: translateX(8.61199px) translateY(-260px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-264px) scale(.34);
			transform: translateX(12.47185px) translateY(-264px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-268px) scale(.33);
			transform: translateX(16.20837px) translateY(-268px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-272px) scale(.32);
			transform: translateX(19.7847px) translateY(-272px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-276px) scale(.31);
			transform: translateX(23.16575px) translateY(-276px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-280px) scale(.3);
			transform: translateX(26.31858px) translateY(-280px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-284px) scale(.29);
			transform: translateX(29.21285px) translateY(-284px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-288px) scale(.28);
			transform: translateX(31.82116px) translateY(-288px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-292px) scale(.27);
			transform: translateX(34.11946px) translateY(-292px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-296px) scale(.26);
			transform: translateX(36.08748px) translateY(-296px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-300px) scale(.25);
			transform: translateX(37.70905px) translateY(-300px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-304px) scale(.24);
			transform: translateX(38.97256px) translateY(-304px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-308px) scale(.23);
			transform: translateX(39.87139px) translateY(-308px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-312px) scale(.22);
			transform: translateX(40.40437px) translateY(-312px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-316px) scale(.21);
			transform: translateX(40.57628px) translateY(-316px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-320px) scale(.2);
			transform: translateX(40.39848px) translateY(-320px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-324px) scale(.19);
			transform: translateX(39.88958px) translateY(-324px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-328px) scale(.18);
			transform: translateX(39.07627px) translateY(-328px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-332px) scale(.17);
			transform: translateX(37.99434px) translateY(-332px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-336px) scale(.16);
			transform: translateX(36.68989px) translateY(-336px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-340px) scale(.15);
			transform: translateX(35.22086px) translateY(-340px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-344px) scale(.14);
			transform: translateX(33.65889px) translateY(-344px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-348px) scale(.13);
			transform: translateX(32.09164px) translateY(-348px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-352px) scale(.12);
			transform: translateX(30.62571px) translateY(-352px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-356px) scale(.11);
			transform: translateX(29.39012px) translateY(-356px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-360px) scale(.1);
			transform: translateX(28.54081px) translateY(-360px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-364px) scale(.09);
			transform: translateX(28.26597px) translateY(-364px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-368px) scale(.08);
			transform: translateX(28.79279px) translateY(-368px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-372px) scale(.07);
			transform: translateX(30.39554px) translateY(-372px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-376px) scale(.06);
			transform: translateX(33.4056px) translateY(-376px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-380px) scale(.05);
			transform: translateX(38.22359px) translateY(-380px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-384px) scale(.04);
			transform: translateX(45.3341px) translateY(-384px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-388px) scale(.03);
			transform: translateX(55.3236px) translateY(-388px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-392px) scale(.02);
			transform: translateX(68.90201px) translateY(-392px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-396px) scale(.01);
			transform: translateX(86.92866px) translateY(-396px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-400px) scale(0);
			transform: translateX(110.44364px) translateY(-400px) scale(0)
		}	}
	@keyframes loader_4 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-4px) scale(.01);
			transform: translateX(3.99334px) translateY(-4px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-8px) scale(.02);
			transform: translateX(7.94677px) translateY(-8px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-12px) scale(.03);
			transform: translateX(11.82081px) translateY(-12px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-16px) scale(.04);
			transform: translateX(15.57673px) translateY(-16px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-20px) scale(.05);
			transform: translateX(19.17702px) translateY(-20px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-24px) scale(.06);
			transform: translateX(22.5857px) translateY(-24px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-28px) scale(.07);
			transform: translateX(25.76871px) translateY(-28px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-32px) scale(.08);
			transform: translateX(28.69424px) translateY(-32px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-36px) scale(.09);
			transform: translateX(31.33308px) translateY(-36px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-40px) scale(.1);
			transform: translateX(33.65884px) translateY(-40px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-44px) scale(.11);
			transform: translateX(35.64829px) translateY(-44px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-48px) scale(.12);
			transform: translateX(37.28156px) translateY(-48px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-52px) scale(.13);
			transform: translateX(38.54233px) translateY(-52px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-56px) scale(.14);
			transform: translateX(39.41799px) translateY(-56px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-60px) scale(.15);
			transform: translateX(39.8998px) translateY(-60px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-64px) scale(.16);
			transform: translateX(39.98294px) translateY(-64px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-68px) scale(.17);
			transform: translateX(39.66659px) translateY(-68px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-72px) scale(.18);
			transform: translateX(38.95391px) translateY(-72px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-76px) scale(.19);
			transform: translateX(37.852px) translateY(-76px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-80px) scale(.2);
			transform: translateX(36.3719px) translateY(-80px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-84px) scale(.21);
			transform: translateX(34.52837px) translateY(-84px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-88px) scale(.22);
			transform: translateX(32.33986px) translateY(-88px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-92px) scale(.23);
			transform: translateX(29.82821px) translateY(-92px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-96px) scale(.24);
			transform: translateX(27.01853px) translateY(-96px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-100px) scale(.25);
			transform: translateX(23.93889px) translateY(-100px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-104px) scale(.26);
			transform: translateX(20.62005px) translateY(-104px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-108px) scale(.27);
			transform: translateX(17.0952px) translateY(-108px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-112px) scale(.28);
			transform: translateX(13.39953px) translateY(-112px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-116px) scale(.29);
			transform: translateX(9.56997px) translateY(-116px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-120px) scale(.3);
			transform: translateX(5.6448px) translateY(-120px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-124px) scale(.31);
			transform: translateX(1.66323px) translateY(-124px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-128px) scale(.32);
			transform: translateX(-2.33497px) translateY(-128px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-132px) scale(.33);
			transform: translateX(-6.30983px) translateY(-132px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-136px) scale(.34);
			transform: translateX(-10.22164px) translateY(-136px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-140px) scale(.35);
			transform: translateX(-14.03133px) translateY(-140px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-144px) scale(.36);
			transform: translateX(-17.70082px) translateY(-144px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-148px) scale(.37);
			transform: translateX(-21.19345px) translateY(-148px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-152px) scale(.38);
			transform: translateX(-24.47432px) translateY(-152px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-156px) scale(.39);
			transform: translateX(-27.51065px) translateY(-156px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-160px) scale(.4);
			transform: translateX(-30.2721px) translateY(-160px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-164px) scale(.41);
			transform: translateX(-32.73108px) translateY(-164px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-168px) scale(.42);
			transform: translateX(-34.86303px) translateY(-168px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-172px) scale(.43);
			transform: translateX(-36.64664px) translateY(-172px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-176px) scale(.44);
			transform: translateX(-38.06408px) translateY(-176px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-180px) scale(.45);
			transform: translateX(-39.1012px) translateY(-180px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-184px) scale(.46);
			transform: translateX(-39.74764px) translateY(-184px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-188px) scale(.47);
			transform: translateX(-39.99693px) translateY(-188px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-192px) scale(.48);
			transform: translateX(-39.84658px) translateY(-192px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-196px) scale(.49);
			transform: translateX(-39.29809px) translateY(-196px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-200px) scale(.5);
			transform: translateX(-38.35695px) translateY(-200px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-204px) scale(.49);
			transform: translateX(-37.03256px) translateY(-204px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-208px) scale(.48);
			transform: translateX(-35.33814px) translateY(-208px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-212px) scale(.47);
			transform: translateX(-33.29063px) translateY(-212px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-216px) scale(.46);
			transform: translateX(-30.91048px) translateY(-216px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-220px) scale(.45);
			transform: translateX(-28.22146px) translateY(-220px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-224px) scale(.44);
			transform: translateX(-25.25043px) translateY(-224px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-228px) scale(.43);
			transform: translateX(-22.02707px) translateY(-228px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-232px) scale(.42);
			transform: translateX(-18.58356px) translateY(-232px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-236px) scale(.41);
			transform: translateX(-14.95428px) translateY(-236px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-240px) scale(.4);
			transform: translateX(-11.17547px) translateY(-240px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-244px) scale(.39);
			transform: translateX(-7.28482px) translateY(-244px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-248px) scale(.38);
			transform: translateX(-3.32114px) translateY(-248px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-252px) scale(.37);
			transform: translateX(.67607px) translateY(-252px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-256px) scale(.36);
			transform: translateX(4.66701px) translateY(-256px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-260px) scale(.35);
			transform: translateX(8.61199px) translateY(-260px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-264px) scale(.34);
			transform: translateX(12.47185px) translateY(-264px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-268px) scale(.33);
			transform: translateX(16.20837px) translateY(-268px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-272px) scale(.32);
			transform: translateX(19.7847px) translateY(-272px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-276px) scale(.31);
			transform: translateX(23.16575px) translateY(-276px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-280px) scale(.3);
			transform: translateX(26.31858px) translateY(-280px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-284px) scale(.29);
			transform: translateX(29.21285px) translateY(-284px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-288px) scale(.28);
			transform: translateX(31.82116px) translateY(-288px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-292px) scale(.27);
			transform: translateX(34.11946px) translateY(-292px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-296px) scale(.26);
			transform: translateX(36.08748px) translateY(-296px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-300px) scale(.25);
			transform: translateX(37.70905px) translateY(-300px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-304px) scale(.24);
			transform: translateX(38.97256px) translateY(-304px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-308px) scale(.23);
			transform: translateX(39.87139px) translateY(-308px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-312px) scale(.22);
			transform: translateX(40.40437px) translateY(-312px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-316px) scale(.21);
			transform: translateX(40.57628px) translateY(-316px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-320px) scale(.2);
			transform: translateX(40.39848px) translateY(-320px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-324px) scale(.19);
			transform: translateX(39.88958px) translateY(-324px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-328px) scale(.18);
			transform: translateX(39.07627px) translateY(-328px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-332px) scale(.17);
			transform: translateX(37.99434px) translateY(-332px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-336px) scale(.16);
			transform: translateX(36.68989px) translateY(-336px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-340px) scale(.15);
			transform: translateX(35.22086px) translateY(-340px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-344px) scale(.14);
			transform: translateX(33.65889px) translateY(-344px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-348px) scale(.13);
			transform: translateX(32.09164px) translateY(-348px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-352px) scale(.12);
			transform: translateX(30.62571px) translateY(-352px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-356px) scale(.11);
			transform: translateX(29.39012px) translateY(-356px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-360px) scale(.1);
			transform: translateX(28.54081px) translateY(-360px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-364px) scale(.09);
			transform: translateX(28.26597px) translateY(-364px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-368px) scale(.08);
			transform: translateX(28.79279px) translateY(-368px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-372px) scale(.07);
			transform: translateX(30.39554px) translateY(-372px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-376px) scale(.06);
			transform: translateX(33.4056px) translateY(-376px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-380px) scale(.05);
			transform: translateX(38.22359px) translateY(-380px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-384px) scale(.04);
			transform: translateX(45.3341px) translateY(-384px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-388px) scale(.03);
			transform: translateX(55.3236px) translateY(-388px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-392px) scale(.02);
			transform: translateX(68.90201px) translateY(-392px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-396px) scale(.01);
			transform: translateX(86.92866px) translateY(-396px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-400px) scale(0);
			transform: translateX(110.44364px) translateY(-400px) scale(0)
		}	}
	@-webkit-keyframes loader_5 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-7px) scale(.01);
			transform: translateX(3.99334px) translateY(-7px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-14px) scale(.02);
			transform: translateX(7.94677px) translateY(-14px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-21px) scale(.03);
			transform: translateX(11.82081px) translateY(-21px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-28px) scale(.04);
			transform: translateX(15.57673px) translateY(-28px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-35px) scale(.05);
			transform: translateX(19.17702px) translateY(-35px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-42px) scale(.06);
			transform: translateX(22.5857px) translateY(-42px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-49px) scale(.07);
			transform: translateX(25.76871px) translateY(-49px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-56px) scale(.08);
			transform: translateX(28.69424px) translateY(-56px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-63px) scale(.09);
			transform: translateX(31.33308px) translateY(-63px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-70px) scale(.1);
			transform: translateX(33.65884px) translateY(-70px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-77px) scale(.11);
			transform: translateX(35.64829px) translateY(-77px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-84px) scale(.12);
			transform: translateX(37.28156px) translateY(-84px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-91px) scale(.13);
			transform: translateX(38.54233px) translateY(-91px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-98px) scale(.14);
			transform: translateX(39.41799px) translateY(-98px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-105px) scale(.15);
			transform: translateX(39.8998px) translateY(-105px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-112px) scale(.16);
			transform: translateX(39.98294px) translateY(-112px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-119px) scale(.17);
			transform: translateX(39.66659px) translateY(-119px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-126px) scale(.18);
			transform: translateX(38.95391px) translateY(-126px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-133px) scale(.19);
			transform: translateX(37.852px) translateY(-133px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-140px) scale(.2);
			transform: translateX(36.3719px) translateY(-140px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-147px) scale(.21);
			transform: translateX(34.52837px) translateY(-147px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-154px) scale(.22);
			transform: translateX(32.33986px) translateY(-154px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-161px) scale(.23);
			transform: translateX(29.82821px) translateY(-161px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-168px) scale(.24);
			transform: translateX(27.01853px) translateY(-168px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-175px) scale(.25);
			transform: translateX(23.93889px) translateY(-175px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-182px) scale(.26);
			transform: translateX(20.62005px) translateY(-182px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-189px) scale(.27);
			transform: translateX(17.0952px) translateY(-189px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-196px) scale(.28);
			transform: translateX(13.39953px) translateY(-196px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-203px) scale(.29);
			transform: translateX(9.56997px) translateY(-203px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-210px) scale(.3);
			transform: translateX(5.6448px) translateY(-210px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-217px) scale(.31);
			transform: translateX(1.66323px) translateY(-217px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-224px) scale(.32);
			transform: translateX(-2.33497px) translateY(-224px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-231px) scale(.33);
			transform: translateX(-6.30983px) translateY(-231px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-238px) scale(.34);
			transform: translateX(-10.22164px) translateY(-238px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-245px) scale(.35);
			transform: translateX(-14.03133px) translateY(-245px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-252px) scale(.36);
			transform: translateX(-17.70082px) translateY(-252px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-259px) scale(.37);
			transform: translateX(-21.19345px) translateY(-259px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-266px) scale(.38);
			transform: translateX(-24.47432px) translateY(-266px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-273px) scale(.39);
			transform: translateX(-27.51065px) translateY(-273px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-280px) scale(.4);
			transform: translateX(-30.2721px) translateY(-280px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-287px) scale(.41);
			transform: translateX(-32.73108px) translateY(-287px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-294px) scale(.42);
			transform: translateX(-34.86303px) translateY(-294px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-301px) scale(.43);
			transform: translateX(-36.64664px) translateY(-301px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-308px) scale(.44);
			transform: translateX(-38.06408px) translateY(-308px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-315px) scale(.45);
			transform: translateX(-39.1012px) translateY(-315px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-322px) scale(.46);
			transform: translateX(-39.74764px) translateY(-322px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-329px) scale(.47);
			transform: translateX(-39.99693px) translateY(-329px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-336px) scale(.48);
			transform: translateX(-39.84658px) translateY(-336px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-343px) scale(.49);
			transform: translateX(-39.29809px) translateY(-343px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-350px) scale(.5);
			transform: translateX(-38.35695px) translateY(-350px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-357px) scale(.49);
			transform: translateX(-37.03256px) translateY(-357px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-364px) scale(.48);
			transform: translateX(-35.33814px) translateY(-364px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-371px) scale(.47);
			transform: translateX(-33.29063px) translateY(-371px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-378px) scale(.46);
			transform: translateX(-30.91048px) translateY(-378px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-385px) scale(.45);
			transform: translateX(-28.22146px) translateY(-385px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-392px) scale(.44);
			transform: translateX(-25.25043px) translateY(-392px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-399px) scale(.43);
			transform: translateX(-22.02707px) translateY(-399px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-406px) scale(.42);
			transform: translateX(-18.58356px) translateY(-406px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-413px) scale(.41);
			transform: translateX(-14.95428px) translateY(-413px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-420px) scale(.4);
			transform: translateX(-11.17547px) translateY(-420px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-427px) scale(.39);
			transform: translateX(-7.28482px) translateY(-427px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-434px) scale(.38);
			transform: translateX(-3.32114px) translateY(-434px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-441px) scale(.37);
			transform: translateX(.67607px) translateY(-441px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-448px) scale(.36);
			transform: translateX(4.66701px) translateY(-448px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-455px) scale(.35);
			transform: translateX(8.61199px) translateY(-455px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-462px) scale(.34);
			transform: translateX(12.47185px) translateY(-462px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-469px) scale(.33);
			transform: translateX(16.20837px) translateY(-469px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-476px) scale(.32);
			transform: translateX(19.7847px) translateY(-476px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-483px) scale(.31);
			transform: translateX(23.16575px) translateY(-483px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-490px) scale(.3);
			transform: translateX(26.31858px) translateY(-490px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-497px) scale(.29);
			transform: translateX(29.21285px) translateY(-497px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-504px) scale(.28);
			transform: translateX(31.82116px) translateY(-504px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-511px) scale(.27);
			transform: translateX(34.11946px) translateY(-511px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-518px) scale(.26);
			transform: translateX(36.08748px) translateY(-518px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-525px) scale(.25);
			transform: translateX(37.70905px) translateY(-525px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-532px) scale(.24);
			transform: translateX(38.97256px) translateY(-532px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-539px) scale(.23);
			transform: translateX(39.87139px) translateY(-539px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-546px) scale(.22);
			transform: translateX(40.40437px) translateY(-546px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-553px) scale(.21);
			transform: translateX(40.57628px) translateY(-553px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-560px) scale(.2);
			transform: translateX(40.39848px) translateY(-560px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-567px) scale(.19);
			transform: translateX(39.88958px) translateY(-567px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-574px) scale(.18);
			transform: translateX(39.07627px) translateY(-574px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-581px) scale(.17);
			transform: translateX(37.99434px) translateY(-581px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-588px) scale(.16);
			transform: translateX(36.68989px) translateY(-588px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-595px) scale(.15);
			transform: translateX(35.22086px) translateY(-595px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-602px) scale(.14);
			transform: translateX(33.65889px) translateY(-602px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-609px) scale(.13);
			transform: translateX(32.09164px) translateY(-609px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-616px) scale(.12);
			transform: translateX(30.62571px) translateY(-616px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-623px) scale(.11);
			transform: translateX(29.39012px) translateY(-623px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-630px) scale(.1);
			transform: translateX(28.54081px) translateY(-630px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-637px) scale(.09);
			transform: translateX(28.26597px) translateY(-637px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-644px) scale(.08);
			transform: translateX(28.79279px) translateY(-644px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-651px) scale(.07);
			transform: translateX(30.39554px) translateY(-651px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-658px) scale(.06);
			transform: translateX(33.4056px) translateY(-658px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-665px) scale(.05);
			transform: translateX(38.22359px) translateY(-665px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-672px) scale(.04);
			transform: translateX(45.3341px) translateY(-672px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-679px) scale(.03);
			transform: translateX(55.3236px) translateY(-679px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-686px) scale(.02);
			transform: translateX(68.90201px) translateY(-686px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-693px) scale(.01);
			transform: translateX(86.92866px) translateY(-693px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-700px) scale(0);
			transform: translateX(110.44364px) translateY(-700px) scale(0)
		}	}
	@keyframes loader_5 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-7px) scale(.01);
			transform: translateX(3.99334px) translateY(-7px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-14px) scale(.02);
			transform: translateX(7.94677px) translateY(-14px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-21px) scale(.03);
			transform: translateX(11.82081px) translateY(-21px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-28px) scale(.04);
			transform: translateX(15.57673px) translateY(-28px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-35px) scale(.05);
			transform: translateX(19.17702px) translateY(-35px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-42px) scale(.06);
			transform: translateX(22.5857px) translateY(-42px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-49px) scale(.07);
			transform: translateX(25.76871px) translateY(-49px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-56px) scale(.08);
			transform: translateX(28.69424px) translateY(-56px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-63px) scale(.09);
			transform: translateX(31.33308px) translateY(-63px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-70px) scale(.1);
			transform: translateX(33.65884px) translateY(-70px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-77px) scale(.11);
			transform: translateX(35.64829px) translateY(-77px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-84px) scale(.12);
			transform: translateX(37.28156px) translateY(-84px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-91px) scale(.13);
			transform: translateX(38.54233px) translateY(-91px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-98px) scale(.14);
			transform: translateX(39.41799px) translateY(-98px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-105px) scale(.15);
			transform: translateX(39.8998px) translateY(-105px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-112px) scale(.16);
			transform: translateX(39.98294px) translateY(-112px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-119px) scale(.17);
			transform: translateX(39.66659px) translateY(-119px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-126px) scale(.18);
			transform: translateX(38.95391px) translateY(-126px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-133px) scale(.19);
			transform: translateX(37.852px) translateY(-133px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-140px) scale(.2);
			transform: translateX(36.3719px) translateY(-140px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-147px) scale(.21);
			transform: translateX(34.52837px) translateY(-147px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-154px) scale(.22);
			transform: translateX(32.33986px) translateY(-154px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-161px) scale(.23);
			transform: translateX(29.82821px) translateY(-161px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-168px) scale(.24);
			transform: translateX(27.01853px) translateY(-168px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-175px) scale(.25);
			transform: translateX(23.93889px) translateY(-175px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-182px) scale(.26);
			transform: translateX(20.62005px) translateY(-182px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-189px) scale(.27);
			transform: translateX(17.0952px) translateY(-189px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-196px) scale(.28);
			transform: translateX(13.39953px) translateY(-196px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-203px) scale(.29);
			transform: translateX(9.56997px) translateY(-203px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-210px) scale(.3);
			transform: translateX(5.6448px) translateY(-210px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-217px) scale(.31);
			transform: translateX(1.66323px) translateY(-217px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-224px) scale(.32);
			transform: translateX(-2.33497px) translateY(-224px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-231px) scale(.33);
			transform: translateX(-6.30983px) translateY(-231px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-238px) scale(.34);
			transform: translateX(-10.22164px) translateY(-238px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-245px) scale(.35);
			transform: translateX(-14.03133px) translateY(-245px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-252px) scale(.36);
			transform: translateX(-17.70082px) translateY(-252px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-259px) scale(.37);
			transform: translateX(-21.19345px) translateY(-259px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-266px) scale(.38);
			transform: translateX(-24.47432px) translateY(-266px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-273px) scale(.39);
			transform: translateX(-27.51065px) translateY(-273px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-280px) scale(.4);
			transform: translateX(-30.2721px) translateY(-280px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-287px) scale(.41);
			transform: translateX(-32.73108px) translateY(-287px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-294px) scale(.42);
			transform: translateX(-34.86303px) translateY(-294px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-301px) scale(.43);
			transform: translateX(-36.64664px) translateY(-301px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-308px) scale(.44);
			transform: translateX(-38.06408px) translateY(-308px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-315px) scale(.45);
			transform: translateX(-39.1012px) translateY(-315px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-322px) scale(.46);
			transform: translateX(-39.74764px) translateY(-322px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-329px) scale(.47);
			transform: translateX(-39.99693px) translateY(-329px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-336px) scale(.48);
			transform: translateX(-39.84658px) translateY(-336px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-343px) scale(.49);
			transform: translateX(-39.29809px) translateY(-343px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-350px) scale(.5);
			transform: translateX(-38.35695px) translateY(-350px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-357px) scale(.49);
			transform: translateX(-37.03256px) translateY(-357px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-364px) scale(.48);
			transform: translateX(-35.33814px) translateY(-364px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-371px) scale(.47);
			transform: translateX(-33.29063px) translateY(-371px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-378px) scale(.46);
			transform: translateX(-30.91048px) translateY(-378px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-385px) scale(.45);
			transform: translateX(-28.22146px) translateY(-385px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-392px) scale(.44);
			transform: translateX(-25.25043px) translateY(-392px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-399px) scale(.43);
			transform: translateX(-22.02707px) translateY(-399px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-406px) scale(.42);
			transform: translateX(-18.58356px) translateY(-406px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-413px) scale(.41);
			transform: translateX(-14.95428px) translateY(-413px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-420px) scale(.4);
			transform: translateX(-11.17547px) translateY(-420px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-427px) scale(.39);
			transform: translateX(-7.28482px) translateY(-427px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-434px) scale(.38);
			transform: translateX(-3.32114px) translateY(-434px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-441px) scale(.37);
			transform: translateX(.67607px) translateY(-441px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-448px) scale(.36);
			transform: translateX(4.66701px) translateY(-448px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-455px) scale(.35);
			transform: translateX(8.61199px) translateY(-455px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-462px) scale(.34);
			transform: translateX(12.47185px) translateY(-462px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-469px) scale(.33);
			transform: translateX(16.20837px) translateY(-469px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-476px) scale(.32);
			transform: translateX(19.7847px) translateY(-476px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-483px) scale(.31);
			transform: translateX(23.16575px) translateY(-483px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-490px) scale(.3);
			transform: translateX(26.31858px) translateY(-490px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-497px) scale(.29);
			transform: translateX(29.21285px) translateY(-497px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-504px) scale(.28);
			transform: translateX(31.82116px) translateY(-504px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-511px) scale(.27);
			transform: translateX(34.11946px) translateY(-511px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-518px) scale(.26);
			transform: translateX(36.08748px) translateY(-518px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-525px) scale(.25);
			transform: translateX(37.70905px) translateY(-525px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-532px) scale(.24);
			transform: translateX(38.97256px) translateY(-532px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-539px) scale(.23);
			transform: translateX(39.87139px) translateY(-539px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-546px) scale(.22);
			transform: translateX(40.40437px) translateY(-546px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-553px) scale(.21);
			transform: translateX(40.57628px) translateY(-553px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-560px) scale(.2);
			transform: translateX(40.39848px) translateY(-560px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-567px) scale(.19);
			transform: translateX(39.88958px) translateY(-567px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-574px) scale(.18);
			transform: translateX(39.07627px) translateY(-574px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-581px) scale(.17);
			transform: translateX(37.99434px) translateY(-581px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-588px) scale(.16);
			transform: translateX(36.68989px) translateY(-588px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-595px) scale(.15);
			transform: translateX(35.22086px) translateY(-595px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-602px) scale(.14);
			transform: translateX(33.65889px) translateY(-602px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-609px) scale(.13);
			transform: translateX(32.09164px) translateY(-609px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-616px) scale(.12);
			transform: translateX(30.62571px) translateY(-616px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-623px) scale(.11);
			transform: translateX(29.39012px) translateY(-623px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-630px) scale(.1);
			transform: translateX(28.54081px) translateY(-630px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-637px) scale(.09);
			transform: translateX(28.26597px) translateY(-637px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-644px) scale(.08);
			transform: translateX(28.79279px) translateY(-644px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-651px) scale(.07);
			transform: translateX(30.39554px) translateY(-651px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-658px) scale(.06);
			transform: translateX(33.4056px) translateY(-658px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-665px) scale(.05);
			transform: translateX(38.22359px) translateY(-665px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-672px) scale(.04);
			transform: translateX(45.3341px) translateY(-672px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-679px) scale(.03);
			transform: translateX(55.3236px) translateY(-679px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-686px) scale(.02);
			transform: translateX(68.90201px) translateY(-686px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-693px) scale(.01);
			transform: translateX(86.92866px) translateY(-693px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-700px) scale(0);
			transform: translateX(110.44364px) translateY(-700px) scale(0)
		}	}
	@-webkit-keyframes loader_6 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@keyframes loader_6 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@-webkit-keyframes loader_7 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@keyframes loader_7 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-6px) scale(.01);
			transform: translateX(3.99334px) translateY(-6px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-12px) scale(.02);
			transform: translateX(7.94677px) translateY(-12px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-18px) scale(.03);
			transform: translateX(11.82081px) translateY(-18px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-24px) scale(.04);
			transform: translateX(15.57673px) translateY(-24px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-30px) scale(.05);
			transform: translateX(19.17702px) translateY(-30px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-36px) scale(.06);
			transform: translateX(22.5857px) translateY(-36px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-42px) scale(.07);
			transform: translateX(25.76871px) translateY(-42px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-48px) scale(.08);
			transform: translateX(28.69424px) translateY(-48px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-54px) scale(.09);
			transform: translateX(31.33308px) translateY(-54px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-60px) scale(.1);
			transform: translateX(33.65884px) translateY(-60px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-66px) scale(.11);
			transform: translateX(35.64829px) translateY(-66px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-72px) scale(.12);
			transform: translateX(37.28156px) translateY(-72px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-78px) scale(.13);
			transform: translateX(38.54233px) translateY(-78px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-84px) scale(.14);
			transform: translateX(39.41799px) translateY(-84px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-90px) scale(.15);
			transform: translateX(39.8998px) translateY(-90px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-96px) scale(.16);
			transform: translateX(39.98294px) translateY(-96px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-102px) scale(.17);
			transform: translateX(39.66659px) translateY(-102px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-108px) scale(.18);
			transform: translateX(38.95391px) translateY(-108px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-114px) scale(.19);
			transform: translateX(37.852px) translateY(-114px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-120px) scale(.2);
			transform: translateX(36.3719px) translateY(-120px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-126px) scale(.21);
			transform: translateX(34.52837px) translateY(-126px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-132px) scale(.22);
			transform: translateX(32.33986px) translateY(-132px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-138px) scale(.23);
			transform: translateX(29.82821px) translateY(-138px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-144px) scale(.24);
			transform: translateX(27.01853px) translateY(-144px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-150px) scale(.25);
			transform: translateX(23.93889px) translateY(-150px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-156px) scale(.26);
			transform: translateX(20.62005px) translateY(-156px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-162px) scale(.27);
			transform: translateX(17.0952px) translateY(-162px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-168px) scale(.28);
			transform: translateX(13.39953px) translateY(-168px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-174px) scale(.29);
			transform: translateX(9.56997px) translateY(-174px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-180px) scale(.3);
			transform: translateX(5.6448px) translateY(-180px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-186px) scale(.31);
			transform: translateX(1.66323px) translateY(-186px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-192px) scale(.32);
			transform: translateX(-2.33497px) translateY(-192px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-198px) scale(.33);
			transform: translateX(-6.30983px) translateY(-198px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-204px) scale(.34);
			transform: translateX(-10.22164px) translateY(-204px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-210px) scale(.35);
			transform: translateX(-14.03133px) translateY(-210px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-216px) scale(.36);
			transform: translateX(-17.70082px) translateY(-216px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-222px) scale(.37);
			transform: translateX(-21.19345px) translateY(-222px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-228px) scale(.38);
			transform: translateX(-24.47432px) translateY(-228px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-234px) scale(.39);
			transform: translateX(-27.51065px) translateY(-234px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-240px) scale(.4);
			transform: translateX(-30.2721px) translateY(-240px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-246px) scale(.41);
			transform: translateX(-32.73108px) translateY(-246px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-252px) scale(.42);
			transform: translateX(-34.86303px) translateY(-252px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-258px) scale(.43);
			transform: translateX(-36.64664px) translateY(-258px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-264px) scale(.44);
			transform: translateX(-38.06408px) translateY(-264px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-270px) scale(.45);
			transform: translateX(-39.1012px) translateY(-270px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-276px) scale(.46);
			transform: translateX(-39.74764px) translateY(-276px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-282px) scale(.47);
			transform: translateX(-39.99693px) translateY(-282px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-288px) scale(.48);
			transform: translateX(-39.84658px) translateY(-288px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-294px) scale(.49);
			transform: translateX(-39.29809px) translateY(-294px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-300px) scale(.5);
			transform: translateX(-38.35695px) translateY(-300px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-306px) scale(.49);
			transform: translateX(-37.03256px) translateY(-306px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-312px) scale(.48);
			transform: translateX(-35.33814px) translateY(-312px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-318px) scale(.47);
			transform: translateX(-33.29063px) translateY(-318px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-324px) scale(.46);
			transform: translateX(-30.91048px) translateY(-324px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-330px) scale(.45);
			transform: translateX(-28.22146px) translateY(-330px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-336px) scale(.44);
			transform: translateX(-25.25043px) translateY(-336px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-342px) scale(.43);
			transform: translateX(-22.02707px) translateY(-342px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-348px) scale(.42);
			transform: translateX(-18.58356px) translateY(-348px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-354px) scale(.41);
			transform: translateX(-14.95428px) translateY(-354px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-360px) scale(.4);
			transform: translateX(-11.17547px) translateY(-360px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-366px) scale(.39);
			transform: translateX(-7.28482px) translateY(-366px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-372px) scale(.38);
			transform: translateX(-3.32114px) translateY(-372px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-378px) scale(.37);
			transform: translateX(.67607px) translateY(-378px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-384px) scale(.36);
			transform: translateX(4.66701px) translateY(-384px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-390px) scale(.35);
			transform: translateX(8.61199px) translateY(-390px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-396px) scale(.34);
			transform: translateX(12.47185px) translateY(-396px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-402px) scale(.33);
			transform: translateX(16.20837px) translateY(-402px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-408px) scale(.32);
			transform: translateX(19.7847px) translateY(-408px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-414px) scale(.31);
			transform: translateX(23.16575px) translateY(-414px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-420px) scale(.3);
			transform: translateX(26.31858px) translateY(-420px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-426px) scale(.29);
			transform: translateX(29.21285px) translateY(-426px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-432px) scale(.28);
			transform: translateX(31.82116px) translateY(-432px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-438px) scale(.27);
			transform: translateX(34.11946px) translateY(-438px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-444px) scale(.26);
			transform: translateX(36.08748px) translateY(-444px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-450px) scale(.25);
			transform: translateX(37.70905px) translateY(-450px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-456px) scale(.24);
			transform: translateX(38.97256px) translateY(-456px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-462px) scale(.23);
			transform: translateX(39.87139px) translateY(-462px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-468px) scale(.22);
			transform: translateX(40.40437px) translateY(-468px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-474px) scale(.21);
			transform: translateX(40.57628px) translateY(-474px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-480px) scale(.2);
			transform: translateX(40.39848px) translateY(-480px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-486px) scale(.19);
			transform: translateX(39.88958px) translateY(-486px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-492px) scale(.18);
			transform: translateX(39.07627px) translateY(-492px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-498px) scale(.17);
			transform: translateX(37.99434px) translateY(-498px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-504px) scale(.16);
			transform: translateX(36.68989px) translateY(-504px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-510px) scale(.15);
			transform: translateX(35.22086px) translateY(-510px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-516px) scale(.14);
			transform: translateX(33.65889px) translateY(-516px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-522px) scale(.13);
			transform: translateX(32.09164px) translateY(-522px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-528px) scale(.12);
			transform: translateX(30.62571px) translateY(-528px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-534px) scale(.11);
			transform: translateX(29.39012px) translateY(-534px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-540px) scale(.1);
			transform: translateX(28.54081px) translateY(-540px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-546px) scale(.09);
			transform: translateX(28.26597px) translateY(-546px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-552px) scale(.08);
			transform: translateX(28.79279px) translateY(-552px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-558px) scale(.07);
			transform: translateX(30.39554px) translateY(-558px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-564px) scale(.06);
			transform: translateX(33.4056px) translateY(-564px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-570px) scale(.05);
			transform: translateX(38.22359px) translateY(-570px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-576px) scale(.04);
			transform: translateX(45.3341px) translateY(-576px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-582px) scale(.03);
			transform: translateX(55.3236px) translateY(-582px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-588px) scale(.02);
			transform: translateX(68.90201px) translateY(-588px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-594px) scale(.01);
			transform: translateX(86.92866px) translateY(-594px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-600px) scale(0);
			transform: translateX(110.44364px) translateY(-600px) scale(0)
		}	}
	@-webkit-keyframes loader_8 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-5px) scale(.01);
			transform: translateX(3.99334px) translateY(-5px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-10px) scale(.02);
			transform: translateX(7.94677px) translateY(-10px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-15px) scale(.03);
			transform: translateX(11.82081px) translateY(-15px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-20px) scale(.04);
			transform: translateX(15.57673px) translateY(-20px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-25px) scale(.05);
			transform: translateX(19.17702px) translateY(-25px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-30px) scale(.06);
			transform: translateX(22.5857px) translateY(-30px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-35px) scale(.07);
			transform: translateX(25.76871px) translateY(-35px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-40px) scale(.08);
			transform: translateX(28.69424px) translateY(-40px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-45px) scale(.09);
			transform: translateX(31.33308px) translateY(-45px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-50px) scale(.1);
			transform: translateX(33.65884px) translateY(-50px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-55px) scale(.11);
			transform: translateX(35.64829px) translateY(-55px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-60px) scale(.12);
			transform: translateX(37.28156px) translateY(-60px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-65px) scale(.13);
			transform: translateX(38.54233px) translateY(-65px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-70px) scale(.14);
			transform: translateX(39.41799px) translateY(-70px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-75px) scale(.15);
			transform: translateX(39.8998px) translateY(-75px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-80px) scale(.16);
			transform: translateX(39.98294px) translateY(-80px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-85px) scale(.17);
			transform: translateX(39.66659px) translateY(-85px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-90px) scale(.18);
			transform: translateX(38.95391px) translateY(-90px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-95px) scale(.19);
			transform: translateX(37.852px) translateY(-95px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-100px) scale(.2);
			transform: translateX(36.3719px) translateY(-100px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-105px) scale(.21);
			transform: translateX(34.52837px) translateY(-105px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-110px) scale(.22);
			transform: translateX(32.33986px) translateY(-110px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-115px) scale(.23);
			transform: translateX(29.82821px) translateY(-115px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-120px) scale(.24);
			transform: translateX(27.01853px) translateY(-120px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-125px) scale(.25);
			transform: translateX(23.93889px) translateY(-125px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-130px) scale(.26);
			transform: translateX(20.62005px) translateY(-130px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-135px) scale(.27);
			transform: translateX(17.0952px) translateY(-135px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-140px) scale(.28);
			transform: translateX(13.39953px) translateY(-140px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-145px) scale(.29);
			transform: translateX(9.56997px) translateY(-145px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-150px) scale(.3);
			transform: translateX(5.6448px) translateY(-150px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-155px) scale(.31);
			transform: translateX(1.66323px) translateY(-155px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-160px) scale(.32);
			transform: translateX(-2.33497px) translateY(-160px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-165px) scale(.33);
			transform: translateX(-6.30983px) translateY(-165px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-170px) scale(.34);
			transform: translateX(-10.22164px) translateY(-170px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-175px) scale(.35);
			transform: translateX(-14.03133px) translateY(-175px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-180px) scale(.36);
			transform: translateX(-17.70082px) translateY(-180px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-185px) scale(.37);
			transform: translateX(-21.19345px) translateY(-185px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-190px) scale(.38);
			transform: translateX(-24.47432px) translateY(-190px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-195px) scale(.39);
			transform: translateX(-27.51065px) translateY(-195px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-200px) scale(.4);
			transform: translateX(-30.2721px) translateY(-200px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-205px) scale(.41);
			transform: translateX(-32.73108px) translateY(-205px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-210px) scale(.42);
			transform: translateX(-34.86303px) translateY(-210px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-215px) scale(.43);
			transform: translateX(-36.64664px) translateY(-215px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-220px) scale(.44);
			transform: translateX(-38.06408px) translateY(-220px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-225px) scale(.45);
			transform: translateX(-39.1012px) translateY(-225px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-230px) scale(.46);
			transform: translateX(-39.74764px) translateY(-230px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-235px) scale(.47);
			transform: translateX(-39.99693px) translateY(-235px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-240px) scale(.48);
			transform: translateX(-39.84658px) translateY(-240px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-245px) scale(.49);
			transform: translateX(-39.29809px) translateY(-245px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-250px) scale(.5);
			transform: translateX(-38.35695px) translateY(-250px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-255px) scale(.49);
			transform: translateX(-37.03256px) translateY(-255px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-260px) scale(.48);
			transform: translateX(-35.33814px) translateY(-260px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-265px) scale(.47);
			transform: translateX(-33.29063px) translateY(-265px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-270px) scale(.46);
			transform: translateX(-30.91048px) translateY(-270px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-275px) scale(.45);
			transform: translateX(-28.22146px) translateY(-275px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-280px) scale(.44);
			transform: translateX(-25.25043px) translateY(-280px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-285px) scale(.43);
			transform: translateX(-22.02707px) translateY(-285px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-290px) scale(.42);
			transform: translateX(-18.58356px) translateY(-290px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-295px) scale(.41);
			transform: translateX(-14.95428px) translateY(-295px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-300px) scale(.4);
			transform: translateX(-11.17547px) translateY(-300px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-305px) scale(.39);
			transform: translateX(-7.28482px) translateY(-305px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-310px) scale(.38);
			transform: translateX(-3.32114px) translateY(-310px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-315px) scale(.37);
			transform: translateX(.67607px) translateY(-315px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-320px) scale(.36);
			transform: translateX(4.66701px) translateY(-320px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-325px) scale(.35);
			transform: translateX(8.61199px) translateY(-325px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-330px) scale(.34);
			transform: translateX(12.47185px) translateY(-330px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-335px) scale(.33);
			transform: translateX(16.20837px) translateY(-335px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-340px) scale(.32);
			transform: translateX(19.7847px) translateY(-340px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-345px) scale(.31);
			transform: translateX(23.16575px) translateY(-345px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-350px) scale(.3);
			transform: translateX(26.31858px) translateY(-350px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-355px) scale(.29);
			transform: translateX(29.21285px) translateY(-355px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-360px) scale(.28);
			transform: translateX(31.82116px) translateY(-360px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-365px) scale(.27);
			transform: translateX(34.11946px) translateY(-365px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-370px) scale(.26);
			transform: translateX(36.08748px) translateY(-370px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-375px) scale(.25);
			transform: translateX(37.70905px) translateY(-375px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-380px) scale(.24);
			transform: translateX(38.97256px) translateY(-380px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-385px) scale(.23);
			transform: translateX(39.87139px) translateY(-385px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-390px) scale(.22);
			transform: translateX(40.40437px) translateY(-390px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-395px) scale(.21);
			transform: translateX(40.57628px) translateY(-395px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-400px) scale(.2);
			transform: translateX(40.39848px) translateY(-400px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-405px) scale(.19);
			transform: translateX(39.88958px) translateY(-405px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-410px) scale(.18);
			transform: translateX(39.07627px) translateY(-410px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-415px) scale(.17);
			transform: translateX(37.99434px) translateY(-415px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-420px) scale(.16);
			transform: translateX(36.68989px) translateY(-420px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-425px) scale(.15);
			transform: translateX(35.22086px) translateY(-425px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-430px) scale(.14);
			transform: translateX(33.65889px) translateY(-430px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-435px) scale(.13);
			transform: translateX(32.09164px) translateY(-435px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-440px) scale(.12);
			transform: translateX(30.62571px) translateY(-440px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-445px) scale(.11);
			transform: translateX(29.39012px) translateY(-445px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-450px) scale(.1);
			transform: translateX(28.54081px) translateY(-450px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-455px) scale(.09);
			transform: translateX(28.26597px) translateY(-455px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-460px) scale(.08);
			transform: translateX(28.79279px) translateY(-460px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-465px) scale(.07);
			transform: translateX(30.39554px) translateY(-465px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-470px) scale(.06);
			transform: translateX(33.4056px) translateY(-470px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-475px) scale(.05);
			transform: translateX(38.22359px) translateY(-475px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-480px) scale(.04);
			transform: translateX(45.3341px) translateY(-480px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-485px) scale(.03);
			transform: translateX(55.3236px) translateY(-485px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-490px) scale(.02);
			transform: translateX(68.90201px) translateY(-490px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-495px) scale(.01);
			transform: translateX(86.92866px) translateY(-495px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-500px) scale(0);
			transform: translateX(110.44364px) translateY(-500px) scale(0)
		}	}
	@keyframes loader_8 {
		0% {
			-webkit-transform: translateX(0px) translateY(0px) scale(0);
			transform: translateX(0px) translateY(0px) scale(0)
		}

		1% {
			-webkit-transform: translateX(3.99334px) translateY(-5px) scale(.01);
			transform: translateX(3.99334px) translateY(-5px) scale(.01)
		}

		2% {
			-webkit-transform: translateX(7.94677px) translateY(-10px) scale(.02);
			transform: translateX(7.94677px) translateY(-10px) scale(.02)
		}

		3% {
			-webkit-transform: translateX(11.82081px) translateY(-15px) scale(.03);
			transform: translateX(11.82081px) translateY(-15px) scale(.03)
		}

		4% {
			-webkit-transform: translateX(15.57673px) translateY(-20px) scale(.04);
			transform: translateX(15.57673px) translateY(-20px) scale(.04)
		}

		5% {
			-webkit-transform: translateX(19.17702px) translateY(-25px) scale(.05);
			transform: translateX(19.17702px) translateY(-25px) scale(.05)
		}

		6% {
			-webkit-transform: translateX(22.5857px) translateY(-30px) scale(.06);
			transform: translateX(22.5857px) translateY(-30px) scale(.06)
		}

		7% {
			-webkit-transform: translateX(25.76871px) translateY(-35px) scale(.07);
			transform: translateX(25.76871px) translateY(-35px) scale(.07)
		}

		8% {
			-webkit-transform: translateX(28.69424px) translateY(-40px) scale(.08);
			transform: translateX(28.69424px) translateY(-40px) scale(.08)
		}

		9% {
			-webkit-transform: translateX(31.33308px) translateY(-45px) scale(.09);
			transform: translateX(31.33308px) translateY(-45px) scale(.09)
		}

		10% {
			-webkit-transform: translateX(33.65884px) translateY(-50px) scale(.1);
			transform: translateX(33.65884px) translateY(-50px) scale(.1)
		}

		11% {
			-webkit-transform: translateX(35.64829px) translateY(-55px) scale(.11);
			transform: translateX(35.64829px) translateY(-55px) scale(.11)
		}

		12% {
			-webkit-transform: translateX(37.28156px) translateY(-60px) scale(.12);
			transform: translateX(37.28156px) translateY(-60px) scale(.12)
		}

		13% {
			-webkit-transform: translateX(38.54233px) translateY(-65px) scale(.13);
			transform: translateX(38.54233px) translateY(-65px) scale(.13)
		}

		14% {
			-webkit-transform: translateX(39.41799px) translateY(-70px) scale(.14);
			transform: translateX(39.41799px) translateY(-70px) scale(.14)
		}

		15% {
			-webkit-transform: translateX(39.8998px) translateY(-75px) scale(.15);
			transform: translateX(39.8998px) translateY(-75px) scale(.15)
		}

		16% {
			-webkit-transform: translateX(39.98294px) translateY(-80px) scale(.16);
			transform: translateX(39.98294px) translateY(-80px) scale(.16)
		}

		17% {
			-webkit-transform: translateX(39.66659px) translateY(-85px) scale(.17);
			transform: translateX(39.66659px) translateY(-85px) scale(.17)
		}

		18% {
			-webkit-transform: translateX(38.95391px) translateY(-90px) scale(.18);
			transform: translateX(38.95391px) translateY(-90px) scale(.18)
		}

		19% {
			-webkit-transform: translateX(37.852px) translateY(-95px) scale(.19);
			transform: translateX(37.852px) translateY(-95px) scale(.19)
		}

		20% {
			-webkit-transform: translateX(36.3719px) translateY(-100px) scale(.2);
			transform: translateX(36.3719px) translateY(-100px) scale(.2)
		}

		21% {
			-webkit-transform: translateX(34.52837px) translateY(-105px) scale(.21);
			transform: translateX(34.52837px) translateY(-105px) scale(.21)
		}

		22% {
			-webkit-transform: translateX(32.33986px) translateY(-110px) scale(.22);
			transform: translateX(32.33986px) translateY(-110px) scale(.22)
		}

		23% {
			-webkit-transform: translateX(29.82821px) translateY(-115px) scale(.23);
			transform: translateX(29.82821px) translateY(-115px) scale(.23)
		}

		24% {
			-webkit-transform: translateX(27.01853px) translateY(-120px) scale(.24);
			transform: translateX(27.01853px) translateY(-120px) scale(.24)
		}

		25% {
			-webkit-transform: translateX(23.93889px) translateY(-125px) scale(.25);
			transform: translateX(23.93889px) translateY(-125px) scale(.25)
		}

		26% {
			-webkit-transform: translateX(20.62005px) translateY(-130px) scale(.26);
			transform: translateX(20.62005px) translateY(-130px) scale(.26)
		}

		27% {
			-webkit-transform: translateX(17.0952px) translateY(-135px) scale(.27);
			transform: translateX(17.0952px) translateY(-135px) scale(.27)
		}

		28% {
			-webkit-transform: translateX(13.39953px) translateY(-140px) scale(.28);
			transform: translateX(13.39953px) translateY(-140px) scale(.28)
		}

		29% {
			-webkit-transform: translateX(9.56997px) translateY(-145px) scale(.29);
			transform: translateX(9.56997px) translateY(-145px) scale(.29)
		}

		30% {
			-webkit-transform: translateX(5.6448px) translateY(-150px) scale(.3);
			transform: translateX(5.6448px) translateY(-150px) scale(.3)
		}

		31% {
			-webkit-transform: translateX(1.66323px) translateY(-155px) scale(.31);
			transform: translateX(1.66323px) translateY(-155px) scale(.31)
		}

		32% {
			-webkit-transform: translateX(-2.33497px) translateY(-160px) scale(.32);
			transform: translateX(-2.33497px) translateY(-160px) scale(.32)
		}

		33% {
			-webkit-transform: translateX(-6.30983px) translateY(-165px) scale(.33);
			transform: translateX(-6.30983px) translateY(-165px) scale(.33)
		}

		34% {
			-webkit-transform: translateX(-10.22164px) translateY(-170px) scale(.34);
			transform: translateX(-10.22164px) translateY(-170px) scale(.34)
		}

		35% {
			-webkit-transform: translateX(-14.03133px) translateY(-175px) scale(.35);
			transform: translateX(-14.03133px) translateY(-175px) scale(.35)
		}

		36% {
			-webkit-transform: translateX(-17.70082px) translateY(-180px) scale(.36);
			transform: translateX(-17.70082px) translateY(-180px) scale(.36)
		}

		37% {
			-webkit-transform: translateX(-21.19345px) translateY(-185px) scale(.37);
			transform: translateX(-21.19345px) translateY(-185px) scale(.37)
		}

		38% {
			-webkit-transform: translateX(-24.47432px) translateY(-190px) scale(.38);
			transform: translateX(-24.47432px) translateY(-190px) scale(.38)
		}

		39% {
			-webkit-transform: translateX(-27.51065px) translateY(-195px) scale(.39);
			transform: translateX(-27.51065px) translateY(-195px) scale(.39)
		}

		40% {
			-webkit-transform: translateX(-30.2721px) translateY(-200px) scale(.4);
			transform: translateX(-30.2721px) translateY(-200px) scale(.4)
		}

		41% {
			-webkit-transform: translateX(-32.73108px) translateY(-205px) scale(.41);
			transform: translateX(-32.73108px) translateY(-205px) scale(.41)
		}

		42% {
			-webkit-transform: translateX(-34.86303px) translateY(-210px) scale(.42);
			transform: translateX(-34.86303px) translateY(-210px) scale(.42)
		}

		43% {
			-webkit-transform: translateX(-36.64664px) translateY(-215px) scale(.43);
			transform: translateX(-36.64664px) translateY(-215px) scale(.43)
		}

		44% {
			-webkit-transform: translateX(-38.06408px) translateY(-220px) scale(.44);
			transform: translateX(-38.06408px) translateY(-220px) scale(.44)
		}

		45% {
			-webkit-transform: translateX(-39.1012px) translateY(-225px) scale(.45);
			transform: translateX(-39.1012px) translateY(-225px) scale(.45)
		}

		46% {
			-webkit-transform: translateX(-39.74764px) translateY(-230px) scale(.46);
			transform: translateX(-39.74764px) translateY(-230px) scale(.46)
		}

		47% {
			-webkit-transform: translateX(-39.99693px) translateY(-235px) scale(.47);
			transform: translateX(-39.99693px) translateY(-235px) scale(.47)
		}

		48% {
			-webkit-transform: translateX(-39.84658px) translateY(-240px) scale(.48);
			transform: translateX(-39.84658px) translateY(-240px) scale(.48)
		}

		49% {
			-webkit-transform: translateX(-39.29809px) translateY(-245px) scale(.49);
			transform: translateX(-39.29809px) translateY(-245px) scale(.49)
		}

		50% {
			-webkit-transform: translateX(-38.35695px) translateY(-250px) scale(.5);
			transform: translateX(-38.35695px) translateY(-250px) scale(.5)
		}

		51% {
			-webkit-transform: translateX(-37.03256px) translateY(-255px) scale(.49);
			transform: translateX(-37.03256px) translateY(-255px) scale(.49)
		}

		52% {
			-webkit-transform: translateX(-35.33814px) translateY(-260px) scale(.48);
			transform: translateX(-35.33814px) translateY(-260px) scale(.48)
		}

		53% {
			-webkit-transform: translateX(-33.29063px) translateY(-265px) scale(.47);
			transform: translateX(-33.29063px) translateY(-265px) scale(.47)
		}

		54% {
			-webkit-transform: translateX(-30.91048px) translateY(-270px) scale(.46);
			transform: translateX(-30.91048px) translateY(-270px) scale(.46)
		}

		55% {
			-webkit-transform: translateX(-28.22146px) translateY(-275px) scale(.45);
			transform: translateX(-28.22146px) translateY(-275px) scale(.45)
		}

		56% {
			-webkit-transform: translateX(-25.25043px) translateY(-280px) scale(.44);
			transform: translateX(-25.25043px) translateY(-280px) scale(.44)
		}

		57% {
			-webkit-transform: translateX(-22.02707px) translateY(-285px) scale(.43);
			transform: translateX(-22.02707px) translateY(-285px) scale(.43)
		}

		58% {
			-webkit-transform: translateX(-18.58356px) translateY(-290px) scale(.42);
			transform: translateX(-18.58356px) translateY(-290px) scale(.42)
		}

		59% {
			-webkit-transform: translateX(-14.95428px) translateY(-295px) scale(.41);
			transform: translateX(-14.95428px) translateY(-295px) scale(.41)
		}

		60% {
			-webkit-transform: translateX(-11.17547px) translateY(-300px) scale(.4);
			transform: translateX(-11.17547px) translateY(-300px) scale(.4)
		}

		61% {
			-webkit-transform: translateX(-7.28482px) translateY(-305px) scale(.39);
			transform: translateX(-7.28482px) translateY(-305px) scale(.39)
		}

		62% {
			-webkit-transform: translateX(-3.32114px) translateY(-310px) scale(.38);
			transform: translateX(-3.32114px) translateY(-310px) scale(.38)
		}

		63% {
			-webkit-transform: translateX(.67607px) translateY(-315px) scale(.37);
			transform: translateX(.67607px) translateY(-315px) scale(.37)
		}

		64% {
			-webkit-transform: translateX(4.66701px) translateY(-320px) scale(.36);
			transform: translateX(4.66701px) translateY(-320px) scale(.36)
		}

		65% {
			-webkit-transform: translateX(8.61199px) translateY(-325px) scale(.35);
			transform: translateX(8.61199px) translateY(-325px) scale(.35)
		}

		66% {
			-webkit-transform: translateX(12.47185px) translateY(-330px) scale(.34);
			transform: translateX(12.47185px) translateY(-330px) scale(.34)
		}

		67% {
			-webkit-transform: translateX(16.20837px) translateY(-335px) scale(.33);
			transform: translateX(16.20837px) translateY(-335px) scale(.33)
		}

		68% {
			-webkit-transform: translateX(19.7847px) translateY(-340px) scale(.32);
			transform: translateX(19.7847px) translateY(-340px) scale(.32)
		}

		69% {
			-webkit-transform: translateX(23.16575px) translateY(-345px) scale(.31);
			transform: translateX(23.16575px) translateY(-345px) scale(.31)
		}

		70% {
			-webkit-transform: translateX(26.31858px) translateY(-350px) scale(.3);
			transform: translateX(26.31858px) translateY(-350px) scale(.3)
		}

		71% {
			-webkit-transform: translateX(29.21285px) translateY(-355px) scale(.29);
			transform: translateX(29.21285px) translateY(-355px) scale(.29)
		}

		72% {
			-webkit-transform: translateX(31.82116px) translateY(-360px) scale(.28);
			transform: translateX(31.82116px) translateY(-360px) scale(.28)
		}

		73% {
			-webkit-transform: translateX(34.11946px) translateY(-365px) scale(.27);
			transform: translateX(34.11946px) translateY(-365px) scale(.27)
		}

		74% {
			-webkit-transform: translateX(36.08748px) translateY(-370px) scale(.26);
			transform: translateX(36.08748px) translateY(-370px) scale(.26)
		}

		75% {
			-webkit-transform: translateX(37.70905px) translateY(-375px) scale(.25);
			transform: translateX(37.70905px) translateY(-375px) scale(.25)
		}

		76% {
			-webkit-transform: translateX(38.97256px) translateY(-380px) scale(.24);
			transform: translateX(38.97256px) translateY(-380px) scale(.24)
		}

		77% {
			-webkit-transform: translateX(39.87139px) translateY(-385px) scale(.23);
			transform: translateX(39.87139px) translateY(-385px) scale(.23)
		}

		78% {
			-webkit-transform: translateX(40.40437px) translateY(-390px) scale(.22);
			transform: translateX(40.40437px) translateY(-390px) scale(.22)
		}

		79% {
			-webkit-transform: translateX(40.57628px) translateY(-395px) scale(.21);
			transform: translateX(40.57628px) translateY(-395px) scale(.21)
		}

		80% {
			-webkit-transform: translateX(40.39848px) translateY(-400px) scale(.2);
			transform: translateX(40.39848px) translateY(-400px) scale(.2)
		}

		81% {
			-webkit-transform: translateX(39.88958px) translateY(-405px) scale(.19);
			transform: translateX(39.88958px) translateY(-405px) scale(.19)
		}

		82% {
			-webkit-transform: translateX(39.07627px) translateY(-410px) scale(.18);
			transform: translateX(39.07627px) translateY(-410px) scale(.18)
		}

		83% {
			-webkit-transform: translateX(37.99434px) translateY(-415px) scale(.17);
			transform: translateX(37.99434px) translateY(-415px) scale(.17)
		}

		84% {
			-webkit-transform: translateX(36.68989px) translateY(-420px) scale(.16);
			transform: translateX(36.68989px) translateY(-420px) scale(.16)
		}

		85% {
			-webkit-transform: translateX(35.22086px) translateY(-425px) scale(.15);
			transform: translateX(35.22086px) translateY(-425px) scale(.15)
		}

		86% {
			-webkit-transform: translateX(33.65889px) translateY(-430px) scale(.14);
			transform: translateX(33.65889px) translateY(-430px) scale(.14)
		}

		87% {
			-webkit-transform: translateX(32.09164px) translateY(-435px) scale(.13);
			transform: translateX(32.09164px) translateY(-435px) scale(.13)
		}

		88% {
			-webkit-transform: translateX(30.62571px) translateY(-440px) scale(.12);
			transform: translateX(30.62571px) translateY(-440px) scale(.12)
		}

		89% {
			-webkit-transform: translateX(29.39012px) translateY(-445px) scale(.11);
			transform: translateX(29.39012px) translateY(-445px) scale(.11)
		}

		90% {
			-webkit-transform: translateX(28.54081px) translateY(-450px) scale(.1);
			transform: translateX(28.54081px) translateY(-450px) scale(.1)
		}

		91% {
			-webkit-transform: translateX(28.26597px) translateY(-455px) scale(.09);
			transform: translateX(28.26597px) translateY(-455px) scale(.09)
		}

		92% {
			-webkit-transform: translateX(28.79279px) translateY(-460px) scale(.08);
			transform: translateX(28.79279px) translateY(-460px) scale(.08)
		}

		93% {
			-webkit-transform: translateX(30.39554px) translateY(-465px) scale(.07);
			transform: translateX(30.39554px) translateY(-465px) scale(.07)
		}

		94% {
			-webkit-transform: translateX(33.4056px) translateY(-470px) scale(.06);
			transform: translateX(33.4056px) translateY(-470px) scale(.06)
		}

		95% {
			-webkit-transform: translateX(38.22359px) translateY(-475px) scale(.05);
			transform: translateX(38.22359px) translateY(-475px) scale(.05)
		}

		96% {
			-webkit-transform: translateX(45.3341px) translateY(-480px) scale(.04);
			transform: translateX(45.3341px) translateY(-480px) scale(.04)
		}

		97% {
			-webkit-transform: translateX(55.3236px) translateY(-485px) scale(.03);
			transform: translateX(55.3236px) translateY(-485px) scale(.03)
		}

		98% {
			-webkit-transform: translateX(68.90201px) translateY(-490px) scale(.02);
			transform: translateX(68.90201px) translateY(-490px) scale(.02)
		}

		99% {
			-webkit-transform: translateX(86.92866px) translateY(-495px) scale(.01);
			transform: translateX(86.92866px) translateY(-495px) scale(.01)
		}

		100% {
			-webkit-transform: translateX(110.44364px) translateY(-500px) scale(0);
			transform: translateX(110.44364px) translateY(-500px) scale(0)
		}	}
	#preloader-percentage {
		position: absolute;
		top: calc(50% - 12px);
		right: 0;
		left: 0;
		color: #fff;
		text-align: center;
		font-size: 13px;
		font-family: 'bentonsanscompbold', sans-serif;
		font-weight: normal;
		font-style: normal;
		z-index: 15
	}
</style>
<nav class="side_navigation"> 
  <div class="side_navigation_media"> 
    <svg version="1.1" class="side_shape_back" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewbox="0 0 130 200" style="enable-background:new 0 0 130 200;" xml:space="preserve"> 
      <path class="side_shape_back_4" d="M130,200V0c0,39.1-66.8,56.7-66.8,105.1C63.2,139.7,130,154.1,130,200z"></path> 
      <path class="side_shape_back_3" d="M130,200V0c0,40.5-26.6,59.5-26.6,100C103.4,154.5,130,162.8,130,200z" data-original="M130,200V0c0,40.5-26.6,59.5-26.6,100C103.4,154.5,130,162.8,130,200z"></path> 
      <path class="side_shape_back_2" d="M130,200V0c0,31.9-13.7,57.8-13.7,100C116.3,137.6,130,173.6,130,200z"></path> 
      <path class="side_shape_back_1" d="M130,200V0c0,40.5,0,59.5,0,100C130,154.5,130,162.8,130,200z"></path> 
    </svg> 
    <svg version="1.1" class="side_shape_front" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 130 200" style="enable-background:new 0 0 130 200;/* display: none; */" xml:space="preserve">
                <path class="side_shape_front_2" d="M130,200V0c0,31.9-87.8,45.3-87.8,100C42.2,151.7,130,172,130,200z"></path>
                <path class="side_shape_front_1" d="M130,200V0c0,31.9,0,57.8,0,100C130,137.6,130,173.6,130,200z" data-original="M130,200V0c0,31.9,0,57.8,0,100C130,137.6,130,173.6,130,200z"></path>
            </svg>
    <svg version="1.1" class="side_navigation_hitarea" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewbox="0 0 100 200" style="enable-background:new 0 0 100 200;" xml:space="preserve"> 
      <path d="M100.1,200.3c-55.3,0-100.1-44.8-100.1-100.1S44.8,0,100.1,0V200.3z"></path> 
    </svg> 
  </div> 
  <ul class="navigation_list nav_main is_active" data-js="main" style="display: block;"> 
    <li class="side_navigation_item is_current" data-target="7up" style="transform: matrix(1, 0, 0, 1, 0, 0);"> <span class="item_dot" data-js="dot-7UP"></span> <a class="item_anchor" style="transform: matrix(1, 0, 0, 1, 200, 0);">7UP</a> </li> 
    <li class="side_navigation_item" data-target="producten" style="transform: matrix(1, 0, 0, 1, 0, 0);"> <span class="item_dot" data-js="dot-Producten"></span> <a class="item_anchor" style="transform: matrix(1, 0, 0, 1, 200, 0);">Producten</a> </li> 
    <li class="side_navigation_item" data-target="geschiedenis" style="transform: matrix(1, 0, 0, 1, 0, 0);"> <span class="item_dot" data-js="dot-Geschiedenis"></span> <a class="item_anchor" style="transform: matrix(1, 0, 0, 1, 200, 0);">Geschiedenis</a> </li> 
    <li class="side_navigation_item" data-target="recept" style="transform: matrix(1, 0, 0, 1, 0, 0);"> <span class="item_dot" data-js="dot-Recept"></span> <a class="item_anchor" style="transform: matrix(1, 0, 0, 1, 200, 0);">Recept</a> </li> 
  </ul> 
  <ul class="navigation_list nav_products" data-js="products" style="display: none;"> 
    <li class="side_navigation_item return" data-target="producten"> <span class="item_arrow"> 
      <svg version="1.1" class="nav_arrow" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewbox="0 0 12.9 10.1" style="enable-background:new 0 0 12.9 10.1;" xml:space="preserve"> 
        <path class="arrow_path" d="M4.9,9.1C3.8,8.1,1.3,5,1.3,5s2.6-3,3.5-4"></path> 
        <line class="arrow_path" x1="2.9" y1="5" x2="11.9" y2="5"></line> 
      </svg> </span> <a class="item_anchor">Producten</a> </li> 
    <li class="side_navigation_item" data-target="producten/regular"> <span class="item_dot" data-js="dot-Regular"></span> <a class="item_anchor">Regular</a> </li> 
    <li class="side_navigation_item" data-target="producten/free"> <span class="item_dot" data-js="dot-Free"></span> <a class="item_anchor">Free</a> </li> 
    <li class="side_navigation_item" data-target="producten/mojito-free"> <span class="item_dot" data-js="dot-Mojito Free"></span> <a class="item_anchor">Mojito Free</a> </li> 
    <li class="side_navigation_item" data-target="producten/lemonlemon"> <span class="item_dot" data-js="dot-Lemon Lemon"></span> <a class="item_anchor">Lemon Lemon</a> </li> 
  </ul> 
  <ul class="navigation_list nav_heritage" data-js="heritage" style="display: none;"> 
    <li class="side_navigation_item return" data-target="geschiedenis"> <span class="item_arrow"> 
      <svg version="1.1" class="nav_arrow" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewbox="0 0 12.9 10.1" style="enable-background:new 0 0 12.9 10.1;" xml:space="preserve"> 
        <path class="arrow_path" d="M4.9,9.1C3.8,8.1,1.3,5,1.3,5s2.6-3,3.5-4"></path> 
        <line class="arrow_path" x1="2.9" y1="5" x2="11.9" y2="5"></line> 
      </svg> </span> <a class="item_anchor">Geschiedenis</a> </li> 
    <li class="side_navigation_item" data-target="geschiedenis/1929"> <span class="item_dot" data-js="dot-1929"></span> <a class="item_anchor">1929</a> </li> 
    <li class="side_navigation_item" data-target="geschiedenis/1950"> <span class="item_dot" data-js="dot-1950"></span> <a class="item_anchor">1950</a> </li> 
    <li class="side_navigation_item" data-target="geschiedenis/heden"> <span class="item_dot" data-js="dot-Heden"></span> <a class="item_anchor">Heden</a> </li> 
    <li class="side_navigation_item" data-target="geschiedenis/intro"> <span class="item_dot" data-js="dot-Intro"></span> <a class="item_anchor">Intro</a> </li> 
  </ul> 
  <ul class="navigation_list nav_recipe" data-js="recipe" style="display: none;"> 
    <li class="side_navigation_item return" data-target="recept"> <span class="item_arrow"> 
      <svg version="1.1" class="nav_arrow" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewbox="0 0 12.9 10.1" style="enable-background:new 0 0 12.9 10.1;" xml:space="preserve"> 
        <path class="arrow_path" d="M4.9,9.1C3.8,8.1,1.3,5,1.3,5s2.6-3,3.5-4"></path> 
        <line class="arrow_path" x1="2.9" y1="5" x2="11.9" y2="5"></line> 
      </svg> </span> <a class="item_anchor">Recept</a> </li> 
    <li class="side_navigation_item" data-target="recept/lemon"> <span class="item_dot" data-js="dot-Lemon"></span> <a class="item_anchor">Lemon</a> </li> 
    <li class="side_navigation_item" data-target="recept/lime"> <span class="item_dot" data-js="dot-Lime"></span> <a class="item_anchor">Lime</a> </li> 
    <li class="side_navigation_item" data-target="recept/bubbels"> <span class="item_dot" data-js="dot-Bubbels"></span> <a class="item_anchor">Bubbels</a> </li> 
  </ul> 
</nav>
<script type="text/javascript">
	var navigationList = document.getElementsByClassName('navigation_list')[0], sideNavigation = document.getElementsByClassName('side_navigation')[0]
	sideNavigation.onmouseout = function(){
		console.log('onmouseout')
		sideNavigation.classList.remove("is_active")
		navigationList.classList.remove("is_open")
		document.getElementsByClassName('side_shape_back_3')[0].setAttribute('d','M130,200V0c0,40.5-26.6,59.5-26.6,100C103.4,154.5,130,162.8,130,200z')
		document.getElementsByClassName('side_shape_front_1')[0].setAttribute('d','M130,200V0c0,31.9,0,57.8,0,100C130,137.6,130,173.6,130,200z')
	}
	sideNavigation.onmouseover = function(){
		console.log('onmouseover')
		sideNavigation.classList.add("is_active")
		navigationList.classList.add("is_open")
		document.getElementsByClassName('side_shape_back_3')[0].setAttribute('d','M130,200V0c0,39.1-66.8,56.7-66.8,105.1C63.2,139.7,130,154.1,130,200z')
		document.getElementsByClassName('side_shape_front_1')[0].setAttribute('d','M130,200V0c0,31.9-87.8,45.3-87.8,100C42.2,151.7,130,172,130,200z')
	}
	document.getElementsByClassName('navigation_list')[0].onclick = function() {
		console.log('jjdj')
		document.getElementsByClassName('side_navigation')[0].className = "side_navigation is_active"
		document.getElementsByClassName('navigation_list')[0].className = "navigation_list nav_main is_active is_open"
	}
	// var t = document.querySelectorAll(".navigation_list .side_navigation_item"), e = window.location.pathname.split("/")
	// for (var i = 0; i < t.length; i++) t[i].classList.remove("is_current");
	// null != document.querySelector('.navigation_list .side_navigation_item[data-target="' + e[1] + '"]') && document.querySelector('.navigation_list .side_navigation_item[data-target="' + e[1] + '"]').classList.add("is_current"),
	// void 0 !== e[2] && null != document.querySelector('.navigation_list .side_navigation_item[data-target="' + e[1] + "/" + e[2] + '"]') && document.querySelector('.navigation_list .side_navigation_item[data-target="' + e[1] + "/" + e[2] + '"]').classList.add("is_current")
</script>

<script type="text/javascript">

function mouseOver()
{
    document.getElementById('div1').style.border = "1px solid red";
    console.log('1')
}
function mouseOut()
{
    document.getElementById('div1').style.border = "1px solid white";
    console.log('2')
}

</script>





<div id="preloader">
  <div class="preloader_inner">
    <div class="preloader_animation">
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="preloader_bubble"></span>
      <span class="loader_circle">
        <svg version="1.1" id="preloader_circle" class="preloader_circle" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
   viewBox="0 0 80 80" style="enable-background:new 0 0 80 80;" xml:space="preserve">
  <path class="preloader_path" d="M40,2.9c20.5,0,37.1,16.6,37.1,37.1S60.5,77.1,40,77.1S2.9,60.5,2.9,40S19.5,2.9,40,2.9"/>
</svg>
      </span>
    </div>
    <div id="preloader-percentage">0 %</div>
  </div>
</div>

