---
title: Simplifying Icon Management in Ext JS
categories:
  - ExtJS
  - Javascript
tags:
  - CSS
  - icon
---

New version of Ext JS, 2.2.1, is announced and we are so happy, aren't we? ;)

Another Ext JS news: [Ext Conference 2009](http://extjs.com/conference/). I wish, I could attend. I hope, I am going to be there in the next conference...

In this short tutorial, I am going to show you to simply the icon management in Ext JS. It is not a complete solution. If you want to see a more professional one, see [Ext.ux.TDGi.iconMgr](http://tdg-i.com/44/extuxtdgiiconmgr-a-utility-class-for-managing-icons-and-css) from TDG innovations.

When you want to use icons in your Ext JS application you either have to use `icon` config option by giving path to your icon or `iconCls` by defining a new CSS class. The latter one is more prefferable way of doing it but it means that you need to define a CSS class for each of your icons. Let's create a new function to make it easy!


```javascript
Ext.ux.Icon = function(icon){
  var path = 'img/icons/';
  if(!Ext.util.CSS.getRule('.icon-'+icon)){
    Ext.util.CSS.createStyleSheet('.icon-'+icon+' { background-image: url('path+icon+'.png) !important; }');
  }
  return 'icon-'+icon;
}
```

Change the value of `path` where your PNG icons are located. Don't tell me you don't hear the famous icon collection from [famfamfam](http://www.famfamfam.com/lab/icons/silk/)!

And call it like:

```javascript
...,
iconCls: Ext.ux.Icon('excel'),
...,
```

It is going to add a new CSS rule `icon-excel` with background-image `excel.png` and add it to the head of your page.

I can hear you say why you have to use PNG extension? You are right, you don't have. Just modify Ext.ux.Icon by adding a second argument, maybe, called as extension and pass the icon's extension:

```javascript
Ext.ux.Icon = function(icon, extension){
  var path = 'img/icons/';
  if(!Ext.util.CSS.getRule('.icon-'+icon)){
    Ext.util.CSS.createStyleSheet('.icon-'+icon+' { background-image: url('path+icon+'.'+extension+') !important; }');
  }
  return 'icon-'+icon;
}
```

```javascript
...,
iconCls: Ext.ux.Icon('excel', 'png'),
...,
```

or by removing the extension part and passing the name of icon with its extension:

```javascript
Ext.ux.Icon = function(icon){
  var path = 'img/icons/';
  if(!Ext.util.CSS.getRule('.icon-'+icon)){
    Ext.util.CSS.createStyleSheet('.icon-'+icon+' { background-image: url('path+icon+') !important; }');
  }
  return 'icon-'+icon;
}
```

```javascript
...,
iconCls: Ext.ux.Icon('excel.png'),
...,
```

Don't use `Ext.ux.Icon` if you are going to use hundreds of CSS rules because each class is defined in its own &#8220;style&#8221; tag and it can affect browser rendering performance.

It's not important what you think, it's important what you do... :)
