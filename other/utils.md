1.input的change实现number类型校验，来源自antd的input的demo
```
  onChange = (index, item, e) => {
        // todo 重新更改 renderItemsConfig值
        const { renderItemsConfig } = this.state
        const targetValue = e.target.value
        const reg = /^-?(0|[1-9][0-9]*)(\.[0-9]*)?$/
        if ((!Number.isNaN(targetValue) && reg.test(targetValue)) || targetValue === '' || targetValue === '-') {
	//回传给input的value值
        }
    };
```
2.
```
  getBase64 = (img, callback) => {
        const reader = new FileReader()
        reader.addEventListener('load', (imgUrl) => callback(reader.result))
        reader.readAsDataURL(img)
    }
    ```
    
 3.
 ```
 ！！！实现一个类eval方法，不过对传参有一定格式要求
 // argsKey:字符串数组，使用   selfEval(`${fn}(container,params)`, ['container', 'params'], container, params)
 
export function selfEval(str, argsKey, ...args) {
    const Fn = Function
    if (argsKey && args) {
        const newFn = new Fn(...argsKey, `return ${str}`)
        return newFn(...args)
    }
    return new Fn(`return ${str}`)()
}
```
4.重写getScript
```
export const getScript = (source, beforeEl, async = true, defer = true) => new Promise((resolve, reject) => {
    let script = document.createElement('script')
    const prior = beforeEl || document.getElementsByTagName('script')[0]

    script.async = async
    //   script.defer = defer
    function onloadHander(_, isAbort) {
        if (isAbort || !script.readyState || /loaded|complete/.test(script.readyState)) {
            script.onload = null
            script.onreadystatechange = null
            script = undefined

            if (isAbort) { reject() } else { resolve() }
        }
    }

    script.onload = onloadHander
    script.onreadystatechange = onloadHander

    script.src = source
    prior.parentNode.insertBefore(script, prior)
})
```