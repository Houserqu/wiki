```js
/**
 * 生成带日期和前缀的 ID
 * @param prefix
 * @returns
 */
export function genId(prefix) {
  const id = [prefix, moment().format('YYYYMMDDHHmmss'), _.random(100000, 999999)].join('');
  if (id.length > 32) {
    throw new Error('ID is too long');
  }
  return id;
}
```

```js
/**
 生成 uuid
 len: 长度
 radix：
*/
export default function (len, radix) {
  let CHARS = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz".split("");
  let chars = CHARS, uuid = [], i;
  radix = radix || chars.length;

  if (len) {
    for (i = 0; i < len; i++)
      uuid[i] = chars[0 | Math.random() * radix];
  } else {
    let r;

    uuid[8] = uuid[13] = uuid[18] = uuid[23] = "-";
    uuid[14] = "4";

    for (i = 0; i < 36; i++) {
      if (!uuid[i]) {
        r = 0 | Math.random() * 16;
        uuid[i] = chars[(i == 19) ? (r & 0x3) | 0x8 : r];
      }
    }
  }
  return uuid.join("");
}
```

