title: CSS实现瀑布流布局
date: 2019-08-27 14:11:20
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

<div class="masonry">
  <div class="item">
    <div class="item__content">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--medium">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--medium">
    </div>
  </div>
  <div class="item">
    <div class="item__content">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--large">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--medium">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
  <div class="item">
    <div class="item__content">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--large">
    </div>
  </div>
  <div class="item">
    <div class="item__content">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--large">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--medium">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--medium">
    </div>
  </div>
  <div class="item">
    <div class="item__content">
    </div>
  </div>
  <div class="item">
    <div class="item__content item__content--small">
    </div>
  </div>
</div>


<style type="text/css">
	@charset "UTF-8";
	@import url("https://fonts.googleapis.com/css?family=PT+Mono");
	body,
	html {
	  position: relative;
	  width: 100%;
	  height: 100%;
	  font-family: "PT Mono", monospace;
	}

	.masonry {
	  -webkit-column-count: 1;
	          column-count: 1;
	  -webkit-column-gap: 0;
	          column-gap: 0;
	  counter-reset: item-counter;
	}
	@media screen and (min-width: 400px) {
	  .masonry {
	    -webkit-column-count: 2;
	            column-count: 2;
	  }
	}
	@media screen and (min-width: 600px) {
	  .masonry {
	    -webkit-column-count: 3;
	            column-count: 3;
	  }
	}
	@media screen and (min-width: 800px) {
	  .masonry {
	    -webkit-column-count: 4;
	            column-count: 4;
	  }
	}
	@media screen and (min-width: 1100px) {
	  .masonry {
	    -webkit-column-count: 5;
	            column-count: 5;
	  }
	}

	.item {
	  box-sizing: border-box;
	  -webkit-column-break-inside: avoid;
	          break-inside: avoid;
	  padding: 10px;
	  counter-increment: item-counter;
	}
	.item__content {
	  position: relative;
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  align-items: center;
	  height: 220px;
	  font-size: 40px;
	  color: #360007;
	  background: currentColor;
	  box-sizing: border-box;
	  color: #720026;
	}
	.item__content:hover {
	  background: #9b0034;
	}
	.item__content:before {
	  position: absolute;
	  top: 0;
	  left: 0;
	  font-size: 13px;
	  width: 2em;
	  height: 2em;
	  line-height: 2em;
	  text-align: center;
	  font-weight: bold;
	  background-color: #222;
	  content: counter(item-counter);
	}
	.item__content:after {
	  color: #1c0004;
	  content: 'ಠ‿ಠ';
	}
	.item__content--small {
	  color: #CE4257;
	  height: 100px;
	}
	.item__content--small:hover {
	  background: #d66274;
	}
	.item__content--small:after {
	  content: '♥◡♥';
	}
	.item__content--medium {
	  color: #FFC093;
	  height: 175px;
	}
	.item__content--medium:hover {
	  background: #ffd8bc;
	}
	.item__content--medium:after {
	  content: '◔ᴗ◔';
	}
	.item__content--large {
	  color: #FF7F51;
	  height: 280px;
	}
	.item__content--large:hover {
	  background: #ff9d7a;
	}
	.item__content--large:after {
	  content: 'ಠ_๏';
	}
</style>
<script>
  window.console = window.console || function(t) {};
</script>
<script>
  if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
  }
</script>