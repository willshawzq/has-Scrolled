# 判断元素是否有滚动条 #
    因为出现滚动条便意味着元素空间将大于其内容显示区域，根据这个现象便可以得到判断是否出现滚动条的规则。
## 判断竖向滚动条 ##
    `el.scrollHeight > el.clientHeight`
    这条规则使用了获取元素不同高度的两个属性：
    
- **scrollHeight**

    指的是元素的内容高度，即如果有滚动条，它的值会等于内容实际的高度加padding值（并不包含border和margin值），在没有内容溢出的情况下它的值等于clientHeight；
- **clientHeight**

    指的是元素的内部高度的px值，包括content和padding值之和，并不包括横向滚动条（horizontal scrollbar）、border和margin的值。

    故而如果每个元素的scrollHeight值大于clientHeight值，则可以说明其出现了竖向滚动条。
## 判断横向滚动条 ##
    `el.scrollWidth > el.clientWidth`
    同样这里使用了获取元素宽度的两个属性：
- **scrollWidth**

    指的是远的内容高度，即它的值会等于内容实际的宽度加上padding值（不包含border和margin值），在没有内容溢出
    的情况下它的值等于clientWidth；
- **clientWidth**

    指的是元素的内部宽度的px值，包括content和padding值之和，并不包括横向滚动条（horizontal scrollbar）、border和margin的值。

    故而如果每个元素的scrollWidth值大于clientWidth值，则可以说明其出现了横向滚动条。
## 特殊情况 ##

       当元素指定了`overflow:hidden`时，是不会出现滚动条的，就算元素的内容尺寸超过了元素尺寸也是不会出现
    滚动条的，所以这里需要对元素是否应用了`overflow:hidden`进行判断。

- **getComputedStyle**

    使用`window`对象下的`getComputedStyle`方法，可以获得元素中最终应用的`CSS`属性值，并且返回一个` CSSStyleDeclaration`对象。故而我们可以通过以下写法来获取最终应用于元素上overflow的值：
        `window.getComputedStyle(el).getPropertyValue("overflow")`

- **currentStyle**

    鉴于`getComputedStyle`IE9以下不支持，故而这里需要使用IE中特有的`currentStyle`来获取最终应用于元素中的`overflow`属性值：
        `el.currentStyle.overflow`
## 总结 ##
    综上可以得出判断元素出现滚动条方法的代码，如下：

    function hasScrolled(el, direction = "vertical") {
        if(direction === "vertical") {
            return el.scrollHeight > el.clientHeight;
        }else if(direction === "horizontal") {
            return el.scrollWidth > el.clientWidth;
        }
     }


在线Demo：[http://codepen.io/willshawzq/pen/PPVdNX](http://codepen.io/willshawzq/pen/PPVdNX "在线Demo")
## 参考文档 ##
[http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/](http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)
[https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth)
