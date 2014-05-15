---
layout: post
title: "Javascript 淺析註冊事件"
date: 2012-08-23T15:10:00+08:00
categories:
 - JavsScript
---

原文：http://www.wowbox.com.tw/blog/article.asp?id=3004 
首先是最常規的方法：
程式碼: 

{% codeblock %}
<p id="para" title="cssrain demo!" onclick="test()" >test</p>
<script>
function test(){
  alert("test");
}
</script>
{% endcodeblock %}
<!-- more -->
當某一天，我們知道JavaScript要跟HTML結構實現分離後，就會改了一種寫法：
程式碼: 

{% codeblock %}
<p id="para" title="cssrain demo!">test</p>
<script>
function test(){
  alert("test");
}
window.onload = function(){
    document.getElementById("para").onclick = test;
}
</script>
{% endcodeblock %}

當我們工作越來越久後，有時候我們需要對某個元素綁定多個相同的事件類型：
程式碼: 

{% codeblock %}
<p id="para" title="cssrain demo!">test</p>
<script>
function test(){
  alert("test");
}

function pig(){
  alert("pig");
}

window.onload = function(){
     document.getElementById("para").onclick = test;
     document.getElementById("para").onclick = pig;
}
</script>
{% endcodeblock %}

如果按照上面的寫法，我們只能輸出第二個函數。
這時候我們需要用到attachEvent方法：
程式碼:

{% codeblock %}
<p id="para" title="cssrain demo!">test</p>
<script>
function test(){
  alert("test");
}

function pig(){
  alert("pig");
}

window.onload = function(){
     document.getElementById("para").attachEvent("onclick",test);
     document.getElementById("para").attachEvent("onclick",pig);
}
</script>
{% endcodeblock %}

在一段時間內，你並沒發現這段代碼有任何錯誤。
某一天，一個名叫firefox的瀏覽器 闖入你的視野，當我們把這段代碼放到firefox中執行後，
發現並不能正常運行。 問題就這樣，越來越多，然而作為一名JS程式設計師，這些都是必須面對的。

為了解決這段代碼的平台兼容性問題，我翻翻手冊，知道了firefox跟ie的區別：
firefox中註冊事件使用：addEventListener方法，同時為了兼容ie，我們必須用到if ... else...
程式碼: 

{% codeblock %}
<p id="para" title="cssrain demo!">test</p>
<script>
function test(){
  alert("test");
}

function pig(){
  alert("pig");
}

window.onload = function(){
         var element =  document.getElementById("para");
         if(element.addEventListener){  // firefox  , w3c
                element.addEventListener("click",test,false);
    element.addEventListener("click",pig,false);
         } else {   // ie 
    element.attachEvent("onclick",test);
    element.attachEvent("onclick",pig);
         }
}
</script>
{% endcodeblock %}

此時，代碼就可以在多個平台上工作了。
但隨著水平的進步，你不滿足每次都去判斷，你想把這個判斷封裝起來，以後可以直接調用：
程式碼: 

{% codeblock %}
<p id="para" title="cssrain demo!">test</p>
<script>
function test(){
  alert("test");
}

function pig(){
  alert("pig");
}

function addListener(element,e,fn){
     if(element.addEventListener){
          element.addEventListener(e,fn,false);
     } else {
          element.attachEvent("on" + e,fn);
     }
}

window.onload = function(){
         var element =  document.getElementById("para");
         addListener(element,"click",test);
         addListener(element,"click",pig);
}
</script>
{% endcodeblock %}

至此，作為一個程式設計師的工作就完了。
中間我們從一個最傳統，最基本的寫法，然後實現Js和HTML的分離，然後又實現對同一個元素註冊多個事件，期間，
我們發現註冊事件的兼容性問題。最後我們對註冊事件的方法進行封裝，方便以後使用。
