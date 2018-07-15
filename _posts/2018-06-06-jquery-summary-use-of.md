---
layout: post
title:  "jQuery use of problem"
categories: JavaScript jQuery
tags: 代码集锦 jQuery
author: 若水三千
---

* content
{:toc}

1.jquery-1.7.2在IE8到IE11中使用ajax和html()无法动态更新HTMLElement元素，
Firefox 60、Chrome 62.0.3202.94中功能正常
```js
function setMenuShortcut() {

    var params = {};
    $.ajax({
        type: "GET",
        url: "http://localhost:8086/menu/getMenuShortcut",
        data: {},
        dataType: "json",
        async: false,
        success: function callback(data) {
            generateMenuList(data);
        }
    });
}

function generateMenuList(data) {
    // check data
    data = data || [];
    // the list of shortcut to access to those menu that response the click event
    $("#function_items").empty();
    var iconList = $("<ol></ol>");
    var addIcon = $('<li><a href="javascript:void(0);" class="ico-add"></a></li>');
    // add listener for click event
    $(addIcon).bind("click", this, moreModule);
    for (var i=0; i<data.returnObject.rows.length; i++) {
        if (data.returnObject.rows[i]['menuUrl'] != '' && data.returnObject.rows[i]['menuUrl'] != null) {
            var item = $("<li></li>");
            var link = $("<a></a>");
            // TODO javascript:openCommonMenu CORS
            $(link).attr("href", "javascript:openCommonMenu(" + data.returnObject.rows[i]['menuCode'] + ")");
            $(link).addClass(data.returnObject.rows[i]['moduleIcon']);
            var text = $("<span></span>").text(data.returnObject.rows[i]['menuDescription']);
            $(link).append(text);
            $(item).append(link);
            $(iconList).append(item);
        }
    }
    $(iconList).append(addIcon);
    $("#function_items").html(iconList);
}
```
调用empty()方法依然无效。设置cache: false，问题修复
```js
function setMenuShortcut() {

    var params = {};
    $.ajax({
        type: "GET",
        url: "http://localhost:8086/menu/getMenuShortcut",
        data: {},
        dataType: "json",
        async: false,
        // fix html() dynamic update html element.
        cache: false,   
        success: function callback(data) {
            generateMenuList(data);
        }
    });
}
```

https://stackoverflow.com/questions/412734/jquery-html-attribute-not-working-in-ie
https://stackoverflow.com/questions/45375945/jquery-propouterhtml-undefined-in-ie

