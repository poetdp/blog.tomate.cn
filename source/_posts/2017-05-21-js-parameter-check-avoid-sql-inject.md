---
title: "js 变量检查（防止sql注入）"
tags:
  - js
  - 变量检查
categories: JavaScript
toc: false
comment: true
notag: false
date: 2017-05-21 14:33:49
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-03f15cb8754529fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

```javascript
/*
 * @param 可能是对象、数组、字符串
 * 检查param中是否含有空白符、引号等，如果有则自动删除这些符号返回一个合法的数据
 */
function check(param) {
    if(typeof param == "object") {
        for(var item in param) {
            if(typeof param[item] == "string")
                param[item] = param[item].replace(/\s|'|"|%|\?/g, "");
        }
    }
    else if(typeof param == "string") {
        param = param.replace(/\s|'|"|%|\?/g, "");
    }
    return param;
}

//test sample

o1 = {a:1, b:"2 3", c:"'user' or 1=1"};
o2 = ["double kill", "triple    kill"];
o3 = "i love    'u'\n";

console.log(o1.a, o1.b, o1.c);
o1 = check(o1);
console.log(o1.a, o1.b, o1.c);

console.log(o2[0], o2[1]);
o2 = check(o2);
console.log(o2[0], o2[1]);

console.log(o3);
o3 = check(o3);
console.log(o3);
```