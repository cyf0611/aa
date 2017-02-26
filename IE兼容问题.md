###绑定事件
>addEventListener

>attachEvent

###解除事件
>removeEventListener

>detachEvent

###获取事件对象
>标准浏览器：通过获取回调函数的参数

>低版本IE：通过window.event

###获取触发事件的DOM元素
>标准浏览器：通过事件对象的target属性 ，比如e.target

>低版本IE：通过事件对象的srcElement来获取：window.event.srcElement

###阻止事件冒泡
>标准浏览器：通过事件对象的stopPropagation()

>低版本IE：通过事件对象的cancelBubble=true
