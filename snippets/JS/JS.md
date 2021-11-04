移动数组元素

```js
function move(arr, nowIndex, toIndex) {
    const tmp = arr[nowIndex]
    arr.splice(nowIndex, 1) // 删除
    arr.splice(toIndex, 0, tmp) // 添加
}
```

[encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

```jsx
function RFC3986UrlEncode(str){
  return encodeURIComponent(str).replace(/[!'()*]/g, function(c) {
    return '%' + c.charCodeAt(0).toString(16).toUpperCase();
  });
}
```

```jsx
// 在 java 等语言中，有些进行的是 HTML4 编码，空格转换成 + 号，而 js 转换成 %20
function javaSdkUrlEncode(str) {
  return encodeURIComponent(str).replace(/%20/g,'+')
}
```

金币格式化

```js
/**
 * 格式化价格
 * 2000099 => 20,000.99 元
 * @param num 单位分
 * @param currencyType
 * @returns {string}
 */
 module.exports = (num, currencyType = null) => {
   let value = Number(num).toFixed(2)
   let parts = value.toString().split(".")

   parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",")

   // 单位， 如果传了币种，则显示单位
   if(currencyType !== null) {
     return parts.join(".") + ' ' +  CURRENCY_UNIT_NAME[currencyType] || '元'
   }

   return parts.join(".")
 }
```

