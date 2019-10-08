title: DropJS文件拖拽上传
date: 2019-06-27 14:11:20
description: 
categories:
- Javascript
tags:
- Javascript
toc: true
author:
comments:
original:
permalink: 
image: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why

<!-- more -->

<div class="drop">
	<div class="dropTop">
		<div class="uploadBtn"></div>
		<div class="setBtn"></div>
	</div>
	<div class="main">
		<div id="box">
			<div class="box">
				<div class="uploads">
					<svg class="icon" style="vertical-align: middle;fill: currentColor;overflow: hidden;" viewBox="0 0 1264 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7483"><path d="M992.171444 312.62966C975.189616 137.155482 827.415189 0 647.529412 0 469.849434 0 323.616239 133.860922 303.679205 306.210218 131.598564 333.839271 0 482.688318 0 662.588235c0 199.596576 161.815189 361.411765 361.411765 361.411765h184.014581V692.705882H294.530793l337.939795-361.411764 337.939796 361.411764H726.132229v331.294118H933.647059v-1.555371c185.470975-15.299199 331.294118-170.426291 331.294117-359.856394 0-168.969898-116.101408-310.367302-272.769732-349.958575z" p-id="7484"></path></svg>
				</div>
				<span class="preloader_bubble"></span>
				<span class="preloader_bubble"></span>
				<span class="preloader_bubble"></span>
				<span class="preloader_bubble"></span>
				<span class="preloader_bubble"></span>
				<span class="preloader_bubble"></span>
				<div class="des">Drop your files to upload</div>
			</div>
		</div>
		<div id="content"></div>
		<div id="recent" class="recent">
			<div class="title">No recents</div>
			<div class="des">Drag & Drop to upload or create a new watch folder for Auto-upload</div>
			<div class="upload">upload</div>
		</div>
	</div>
</div>


<style type="text/css">
	div{
		color: #898c90;
	}
	.box, .recent{
		/*width: 300px;
		height: 300px;
		border:1px dashed #000;*/
		position:absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		/*text-align:center;*/
		/*display:none;*/
		animation-name:mymove;
		animation-duration: 2s
	}
	.box .uploads{
		width: 100px;
		height: 100px;
		background: #5826e9;
		border-radius: 50%;
		margin: auto;
		margin-bottom: 50px;
		position: relative;
    z-index: 111;
	}
	.drop{
		width: 400px;
    height: 500px;
    position:absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    margin: auto;
		box-shadow: 0px 10px 21px rgba(0,0,0,0.07);
	}
	.icon{
		color: #FFF;
		width: 50px;
		height: 50px;
		margin: 25px;
	}
	#box{
		width: 100%;
		height: 100%;
		position:absolute;
		display:none;
		/*display: block;*/
	}
	.recent{
		display: block;
	}
	.title{
		text-align: center;
    font-size: 20px;
    color: #000;
    line-height: 50px;
	}
	.recent .des{
		font-size: 12px;
    line-height: 20px;
	}
	.upload{
		width: 120px;
    height: 50px;
    line-height: 50px;
    text-align: center;
    color: #FFF;
    background: #5826e9;
    border-radius: 10px;
    margin: auto;
    margin-top: 20px;
	}
	.preloader_bubble {
		position: absolute;
		top: 50px;
		left: 50px;
		background-color: #5826e9;
		border-radius: 50%;
		/*transform: scale(0);*/
		/*animation: popup 0.6s 0.3s cubic-bezier(0.24, 1.65, 0.425, 0.92) forwards;*/
		width: 5px;
		height: 5px;
		animation-name: loader_1;
		animation-duration: 2.2s;
		animation-delay: 0s;
		animation-iteration-count: infinite;
		animation-timing-function: linear;
		animation-play-state: running;
		margin-left: 35px;
	}
	.preloader_bubble:nth-child(2) {
		background-color: #fd0;
		margin-left: 45px;
		width: 4px;
		height: 4px;
		animation-delay: 0.5s;
	}
	.preloader_bubble:nth-child(3) {
		background-color: #2d1575;
		margin-left: 49px;
		animation-delay: 0.6s;
	}
	.preloader_bubble:nth-child(4) {
		background-color: #2d1575;
		margin-left: 27px;
		animation-delay: 0.7s;
		width: 3px;
		height: 3px;
	}
	.preloader_bubble:nth-child(5) {
		background-color: #2d1575;
		margin-left: 50px;
		animation-delay: 1s;
	}
	.preloader_bubble:nth-child(6) {
		background-color: #1d0e48;
		margin-left: 14px;
		animation-delay: 0.1s;
	}
	@keyframes loader_1 {
		0%{
			transform: translateX(0px) translateY(50px) scale(1);
			opacity: 1;
		}
		100%{
			transform: translateX(0px) translateY(100px) scale(1);
			opacity: 0;
		}
	}
	@keyframes popup {
		100% {
			transform: scale(1)
		}
	}
	@keyframes mymove{
		from{
			margin-top: 50px;
		}
		/*执行动画的初始位置*/
		to{
			margin-top: 0px;
		}
		/*动画结束位置*/
		0%{
			opacity: 0.1;
		/*初始状态 透明度为10%*/
		}
		50%{
			opacity: 0.5;
		/*中间状态 透明度为50%*/
		}
		100%{
			opacity: 1;
		/*结尾状态 不透明*/
		}
	}
	.files{
		margin: 20px;
	}
	.files .image{
		float: left;
		width: 100px;
		height: 50px;
		border-radius: 6px;
		background-position: center;
		background-size: 100%;
	}
	.left{
		float: left;
		width: 200px;
		margin-left: 10px;
	}
	.h1{
		font-size: 16px;
    line-height: 30px;
    color: #000;
    margin: 0;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
	}
	.h2{
		font-size: 14px;
		margin: 0;
	}
	.loading{
		float: right;
	}
</style>

<script>
	window.onload = function () {
		var oBox = document.getElementById('box')
		var oRecent = document.getElementById('recent')
		var oContent = document.getElementById('content')
		var oM = document.getElementById('m1')
		var timer = null
		document.ondragover = function(){
			clearTimeout(timer)
			timer = setTimeout(function(){
				oBox.style.display = 'none'
				oRecent.style.display = 'block'
			},200)
			oBox.style.display = 'block'
			oRecent.style.display = 'none'
		}
		//进入子集的时候 会触发ondragover 频繁触发 不给ondrop机会
		oBox.ondragenter = function(){
			// oBox.style.display = 'block'
			// oRecent.style.display = 'none'
			// oBox.innerHTML = '请释放鼠标'
		}
		oBox.ondragover = function(){
			return false
		}
		oBox.ondragleave = function(){
			// oBox.style.display = 'none'
			// oRecent.style.display = 'block'
			// oBox.innerHTML = '请将文件拖拽到此区域'
		}
		oBox.ondrop = function(ev){
			var oFile = ev.dataTransfer.files[0]
			console.log(oFile)
			var reader = new FileReader()
			//读取成功
			reader.onload = function(){
				console.log(reader)
				oRecent.style.display = 'none'
				oContent.innerHTML = `
				<div class="files">
					<div class="image" style="background-image: url(${reader.result})"></div>
					<div class="left">
						<p class="h1">${oFile.name}</p>
						<p class="h2">${oFile.size}字节</p>
					</div>
					<div class="loading"></div>
				</div>
				`
			}
			reader.onloadstart = function(){
				console.log('读取开始')
			}
			reader.onloadend = function(){
				console.log('读取结束')
			}
			reader.onabort = function(){
				console.log('中断')
			}
			reader.onerror = function(){
				console.log('读取失败')
			}
			reader.onprogress = function(ev){
				var scale = ev.loaded/ev.total
				if(scale>=0.5){
					console.log(1)
					reader.abort()
				}
				oM.value = scale*100
			}
			reader.readAsDataURL(oFile,'base64')
			return false
		};
	};
</script>