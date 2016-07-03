# MIP 校验list（正在使用）

## MIP HTML 标签和属性错误

### 1. 缺少强制性标签

|提示|MANDATORY_TAG_MISSING|
|---|---|
|错误说明|"The mandatory tag '%1' is missing or incorrect."|
|错误说明|强制性标签'xxx'缺失或错误|
|修复方法|添加（或者更正）强制性html标签|

在MIP HTML中，强制性标签包括：

- `<!doctype html>`

- `<html mip>`或`<html>`
	 
- `<head>`
	 
- `<meta charset="utf-8">`
	 
- `<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">`
	 
- `<script async src="https://m.baidu.com/miphtml/v0.js"></script>`
	 
- `<link rel="stylesheet" type="text/css" href="//m.baidu.com/static/ala/sf/static/css/miphtml_xxxxxx.css">`xxx会根据版本不同而不同
	 
- `<script src="//m.baidu.com/static/ala/sf/static/js/miphtml_main_xxxxxx.js"></script>`xxx会根据版本不同而不同
	 
- `<body>`
	 
- 也就是说上述标签如果缺失或者错误需要给出提示，并且校验不能通过。

<font color="red">
	 
**注意**：
	 
1. 上述强制标签没有顺序或者位置的要求<br>
2. charset属性utf-8可以小写，也可以大写成UTF-8<br>
3. 其他强制小写<br>
4. 无单引号或者双引号限制（单引号或者双休引号均可）<br>
5. 属性无顺序要求

</font>

### 2. 禁用标签

|提示|DISALLOWED_TAG|	 
|---|---|
|错误说明|"The tag '%1' is disallowed."|
|错误说明|禁止使用'xx'标签|
|修复方法|删除禁用标签|

目前mip中标签使用规则：

禁止使用标签有：

- frame	 
- frameset	 
- object
- param	 
- applet
- embed
- form
- input
- input
- textarea
- select
- option

如果有如下标签需要进行替换

标签|替换后标签
----|----
img|mip-img
video|mip-video（暂未开放）
audio|mip-audio（暂未开放）
iframe|mip-iframe

其他说明：

- style：仅允许在head标签中的style标签中使用

<font color="red">
-**注意**：

1. 可以把img/video/audio/iframe视为禁用标签

</font>

### 3. 无效属性值

|提示|INVALID_ATTR_VALUE|
|---|---|
|错误说明|"The attribute '%1' in tag '%2' is set to the invalid value '%3'."|
|错误说明|标签'xx'中的属性'xx'的属性值'xx'无效|
|修复方法|修改为有效属性值|

当html标签有属性值不正确的时候，会报这个错误。mip中需要注意的有：

- a：href属性不允许使用javascript:协议，

- a：target属性需要设置为`_blank`

- mip-img
    - src：必须是一个url
    - data-carousel：目前只有carousel属性值

- mip-pix
    - src：必须是一个支持https的地址url，
    - 如果不支持https适用百度提供的https代理，url中带t={TIME}&title={TITLE}&host={HOST}&from=baidu"

- mip-ad
    - tpl：onlyImg, noneImg, moreImg(只能是这三个)
    - src：必须是url
    - data-size："1242 180", 两个数字中间用空格隔开
    - data-img：必须是url

- 其他html基本页面属性规范不变

<font color="red">

**注意**：

1. MIP HTML中的url强制是https的<br>

2. a:<br>
    - `<a href="javascript:xxx()"></a>` 错<br>
    - `<a href="xxx" target="_blank"></a>` 对

</font>

### 4. 属性值的无效值

|提示|INVALID_PROPERTY_VALUE_IN_ATTR_VALUE|
|---|---|
|错误说明|"The property '%1' in attribute '%2' in tag '%3' is set to '%4', which is invalid."|
|错误说明|标签'xx'中存在属性'yy','yy'中存在属性'zz'，属性'zz'的属性值'aa'无效|
|修复方法|更正无效属性值|

可能出现属性值的无效值的情况：

- `<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">`
    - width的属性值device-width
    - minimum-scale的属性值1
    - initial-scale的属性值1

<font color="red">

**注意**：

1. 除上述给出的值外均为无效值

</font>

### 5. 无效的URL协议

|提示|INVALID_URL_PROTOCOL|
|---|---|
|错误说明|Invalid URL protocol '%3:' for attribute '%1' in tag '%2'.|
|错误说明|表填'xx'中的属性'xx'的url协议'xx'是无效的|
|修复方法|添加有效协议。如将http改为https|

<font color="red">

**注意**：

1. mip html中所有的**资源**url必须是https的<br>
2. 包括mip页面本身也必须是https的

</font>

### 6. 缺少强制性属性

|提示|MANDATORY_ONEOF_ATTR_MISSING|
|---|---|
|错误说明|"The tag '%1' is missing a mandatory attribute - pick one of %2."|
|错误说明|标签'xx'的强制性属性'xx'缺失|
|修复方法|添加正确是属性|

mip html中具有强制性属性的标签及其强制性属性有：

- mip-img
    - src
- mip-pix
    - src
- mip-baidu-tj
    - token
- mip-ad
    - tpl
    - src
    - data-size
    - data-img

### 7. 直接父标签错误

|提示|WRONG_PARENT_TAG|
|---|---|
|错误说明|"The parent tag of tag '%1' is '%2', but it can only be '%3'."|
|错误说明|标签'a'的直接父标签应该是'b'，而不是'c'|
|修复方法|添加所需的父标签|

有一些标签有制定的直接父标签，如下示例给出了每个标签必须的直接父标签：

- **!doctype** 的直接父标签是 **root**
- **head** 的直接父标签是 **html**
- **body** 的直接父标签是 **html**
- **link** 的直接父标签是 **head**
- **meta** 的直接父标签是 **head**
- **style mip-custom** 的直接父标签是 **head**
- **style** 的直接父标签是 **boilerplate**
- **script** 的直接父标签是 **head**

### 8. 非法父级标签

|提示|DISALLOWED_TAG_ANCESTOR|
|---|---|
|错误说明|"The tag '%1' may not appear as a descendant of tag '%2'."|
|错误说明|标签'a'不应该是标签'b'的子标签|
|修复方法|删除非法嵌套标签|

如：

- `<body>`的子标签写在了`<head>`中

### 9. 强制父级标签

|提示|MANDATORY_TAG_ANCESTOR|
|---|---|
|错误说明|"The tag '%1' may only appear as a descendant of tag '%2'."|
|错误说明|M标签'a'只能是标签'b'的子级标签|
|修复方法|删除标签或者给标签添加正确的父级标签|

- img 必须是noscript的子级标签
- video 必须是noscript的子级标签
- audio 必须是noscript的子级标签
- noscript必须是body的子级标签

### 10. 唯一标签重复
|提示|DUPLICATE_UNIQUE_TAG|
|---|---|
|错误说明|"The tag '%1' appears more than once in the document."|
|错误说明|标签'xx'只能出现一次|
|修复方法|删除多余的标签|

一份html中，有的标签具有唯一性，也就是说只能出现一次，当html中有重复的唯一标签的时候，应该报错。

以下是唯一标签列表：

- `<doctype html>`
- `<html mip>`
- `<head>`
- `<link rel=canonical href=...>`
- `<link rel=amphtml href=...>`
- `<meta charset="utf-8">`
- `<meta viewport>`
- `<style mip-custom>`
- `<script async src="https://m.baidu.com/miphtml/v0.js"></script>`
- `<body>`