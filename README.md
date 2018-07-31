# 兼容性问题汇总
## 移动端兼容性  
### IOS将数字当做电话号码：meta标签telephone=no  
### andriod对邮箱的识别：meta email=no  
### flex：-webkit-box  
### ios fixed定位元素抖动：-webkit-overflow-scroll:touch  
### 多行省略：
```javascript
.overflow-hidden{
display: box !important;
display: -webkit-box !important;
overflow: hidden;
text-overflow: ellipsis;
-webkit-box-orient: vertical;
-webkit-line-clamp: 4;/*第几行出现省略号*/
/*text-align:justify;不能和溢出隐藏的代码一起写，会有bug*/
}
```
### ios fixed输入框focus吊起输入法：
```javascript
window.addEventListener('resize', function() {
    if(document.activeElement.tagName === 'INPUT' || document.activeElement.tagName === 'TEXTAREA') {
        window.setTimeout(function() {
          if('scrollIntoView' in document.activeElement) {
            document.activeElement.scrollIntoView();
          } else {
            document.activeElement.scrollIntoViewIfNeeded();
          }
        }, 0);
    }
});
```
### 去除默认样式：-webkit-appearance: none;  
### 禁用手机页面缓存：
```javascript
<meta http-equiv="Cache-Control"content="no-cache"/>
```
### ios输入字母，首字母默认大写：
```javascript
<input type="text"autocapitalize="off"/>
```
### type为search，带有删除图标：
```javascript
#Search::-webkit-search-cancel-button{
  display:none; 
}
```
### 移动端click延迟300ms，使用tap，引入fastclick.js或tap.js
### 点透问题
#### 原因：
touchstart 早于 touchend 早于click，上层浮动层消失，300ms后自动触发下层click，触发底层元素事件。
#### 解决方法：
fastclick.js、使用touchEnd替换click
### ios去点击效果：-webkit-tap-highlight-color：rgba(255,255,255,0)
### button标明type，否则会出现自动提交表单的bug  
### 弹层的关闭事件容易触发弹层关闭后下一层的事件所以要给弹层关闭事件加上event.preventDefault()
### 弹层后禁止滚动：给弹层添加mousemove事件event.preventDefault()  
## 浏览器兼容
### 不同浏览器padding、margin不同：*{margin：;0padding:0}  
### 图片img标签默认有间距：float   
### css hack做浏览器兼容，ie6识别*和_,ie7识别*,其他识别原属性  
#### 实例：
```javascript
height:100px;
*+height:200px;
_height:300px;
```
ie6识别为300px,ie7识别为200px，其他是识别为100px。  
### 外部标签不要定死高度，并加上overflow：hidden以达到高度自适应。  
### 透明opacityIE不支持，IE用filter  
#### 实例：

```javascript
{
	opacity:0.5;
	filter:alpha(opacity=0.5);
}
### IE6无法设置1px高度：设置overflow：hidden或line-height：1px  
### form标签IE会有margin  
