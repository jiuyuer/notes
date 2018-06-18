---
title: JavaScript 异步上传文件
date: 2012-10-12 15:50:39
tags: 
- JavaScript
categories: 
- 技术渣
---

## 起因
项目中做到了头像上传的功能.因为不可能修改头像就把整个表单提交,所以必须要使用 AJAX 来实现异步上传文件.

## 经过
服务端只要获取到客户端文件的本地路径,然后使用文件流来实现文件操作就可以了.
主要还是在浏览器端获取文件的本地路径和预览功能.
IE 浏览器从 IE6 开始已经不能使用 input.value 直接获取 input:file 控件的本地路径
其他浏览器比如 chrom 和 FF 等都不能直接使用 input.value 获取文件的本地路径.
那么只能使用别的方法实现异步上传文件功能.
首先声明 IE6 不考虑
chrome 和 firefox 因为对 HTML5 支持比较好.所以可以使用 HTML5 中的 files 和 FileReader 对象来实现图片预览功能。如下：

```javascript
var fileList = obj.files;
var imageType = /image.*/;
for (var i = 0; i < fileList.length; i++) {
  var file = fileList[i];
  if (!file.type.match(imageType)) {
    continue;
  }

  var reader = new FileReader();
  reader.onload = function(e) {
    fileName = e.target.result; //Data URI格式
    img.src = fileName; //给img.src赋值
  };
  reader.readAsDataURL(file); //转换成Data URI格式
}
```

<!-- more -->

IE7-IE9 使用

```javascript
this.select();
this.blur();
var fileName = document.selection.createRange().text;
```

来获取文件的本地路径.
然后是用图片预览,因为 IE7-IE9 中的 img 控件的 src 属性已经不能直接使用本地路径来显示图片.所以使用滤镜来实现

```javascript
divShowImage.setAttribute(
  'style',
  'filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale);width:300px; height:300px;'
);
divShowImage.filters.item(
  'DXImageTransform.Microsoft.AlphaImageLoader'
).src = fileName;
img.setAttribute('style', 'display:none'); //隐藏IMG避免在图片的左上角出现一个小叉叉.
```

---

## 20121009 更新

然后是上传..在这里遇到了最大的问题...其实在之前已经遇到过这个问题...但是都先放过去.等要用到的时候再去实现..

就是 chrome 居然无法获取到图片的本地路径.因为不想提交表单域.网上还是提供了使用 js 中的 XMLHTTPResponse 对象来实现 ajax 直接提交图片的二进制码.

因为以前都是使用 jq 来实现 ajax 的.所以对于 XMLHTTPResponse 对象非常不熟悉.导致在.ashx 中都不知道如何获取数据.尝试了多次..暂时没有结果.这时候我又开始思考是不是应该继续下去.因为已经感觉到复杂了..这么一个异步上传..在理想中不应该是如此复杂,那么就应该考虑自己的思路是不是出现了问题,是不是能换个思路进行下去.

1.  考虑使用 IFrame 中嵌入上传的页面来实现异步上传.
2.  早先考虑过的使用 falsh 插件.但是还是感觉不好..因为觉得可以用 js+ajax 实现.
3.  还想到 webcjs 中使用的异步上传,使用表单域提交,因为其他数据都是通过无表单域的 AJAX 提交的.所以页面的表单域可以留给上传文件.
4.  继续尝试取得提交到服务端的 XMLHTTPResponse 对象.


决定了.. 先使用第三条解决方案.
终于完成异步头像上传的全部功能...还是使用了客户端提交表单,然后服务端 context.Request.Files 来获取文件属性.并且使用 jquery.form.js 来实现异步提交表单.
主要问题还是服务端获取不到 Files 对象.form 中必须有 enctype="multipart/form-data"
然后 input:file 控件中必须要有 runat="server"
然后才可以在.ashx 文件中获取到 Request.Files;
后面的保存和修改数据库信息已经不存在问题了.

## 总结
就是感觉 HTML5 兼容性太差.各种不确定.有些属性不是这个浏览器不支持就是那个浏览器不支持.
预览图片的还是使用 HTML5 中 files 对象来转换成 Data URI 来赋值到 src 属性上.
然后 IE 的预览图片还是使用滤镜来实现.
