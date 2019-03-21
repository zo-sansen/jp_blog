---
title: canvas图片下载
date: 2019-2-21
author: alanJiang
tags:
    - JS
categories:
    - JS
thumbnail:  
blogexcerpt: canvas图片下载
```javascript
var canvasElement = document.getElementById(id);

var MIME_TYPE = "image/png";

var imgURL = canvasElement.toDataURL(MIME_TYPE);

var dlLink = document.createElement('a');
dlLink.download = fileName;
dlLink.href = imgURL;
dlLink.dataset.downloadurl = [MIME_TYPE, dlLink.download, dlLink.href].join(':');

document.body.appendChild(dlLink);
dlLink.click();
document.body.removeChild(dlLink);
```

