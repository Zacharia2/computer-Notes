```javascript
document.oncontextmenu = function(evt) {evt = evt||window.event;evt.returnValue=false;}//屏蔽鼠标右键 
document.onselectstart = function(evt){evt = evt||window.event;evt.returnValue=false;}//屏蔽鼠标选择
window.onhelp = function() {return false;} //屏蔽F1帮助 
document.onmousewheel = function(evt)//屏蔽Shift+滚轮,Ctrl+滚轮
{ 
	evt = evt||window.event;
	if(evt.shiftKey || evt.ctrlKey)
	{
		evt.keyCode=0; 
		evt.returnValue=false; 		
	}
}
document.onkeydown = function(evt)
{ 
  evt = evt||window.event;
  if (evt.keyCode==27){evt.keyCode=0;evt.returnValue=false;}  //屏蔽ESC
  if (evt.keyCode==114){evt.keyCode=0;evt.returnValue=false;}  //屏蔽F3
  if (evt.keyCode==116){evt.keyCode=0;evt.returnValue=false;}  //屏蔽F5
  if (evt.keyCode==122){evt.keyCode=0;evt.returnValue=false;}  //屏蔽F11
  if (evt.keyCode==123){evt.keyCode=0;evt.returnValue=false;}  //屏蔽F12
  if(evt.ctrlKey && evt.keyCode==67) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+c
  if(evt.ctrlKey && evt.keyCode==86) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+v
  if(evt.ctrlKey && evt.keyCode==70) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+f
  if(evt.ctrlKey && evt.keyCode==87) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+w
  if(evt.ctrlKey && evt.keyCode==69) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+e
  if(evt.ctrlKey && evt.keyCode==72) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+h
  if(evt.ctrlKey && evt.keyCode==73) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+i
  if(evt.ctrlKey && evt.keyCode==79) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+o
  if(evt.ctrlKey && evt.keyCode==76) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+l
  if(evt.ctrlKey && evt.keyCode==80) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+p
  if(evt.ctrlKey && evt.keyCode==66) {evt.keyCode=0;evt.returnValue=false;}	//屏蔽 Ctrl+b
  if (evt.ctrlKey && evt.keyCode==78) {evt.keyCode=0;evt.returnValue=false;}  //屏蔽 Ctrl+n
  if (evt.shiftKey && evt.keyCode==121){evt.keyCode=0;evt.returnValue=false;}  //屏蔽 shift+F10 
  if (evt.srcElement.tagName == "A" && window.evt.shiftKey) {evt.keyCode=0;evt.returnValue=false;}             //屏蔽 shift 加鼠标左键新开一网页 
}

document.onmousedown = function(evt)
{
	try
	{
		evt = evt||window.event;
		if(evt.button==4){evt.keyCode=0;evt.returnValue=false;}	//屏蔽鼠标中键
	}
	catch(e)
	{}	
}
```

如果你想使用鼠标右键以及快捷键，可以设置浏览器禁用 js 脚本。但考试系统不建议这样做，文库这些可以。