cookie 获取和设置封装

```js
export default {
    get: function (name) {
      let ret = document.cookie.match(new RegExp("(?:^|;\\s)" + name + "=(.*?)(?:;\\s|$)"));
      return ret ? ret[1] : "";
    },
    set: function (key, value, opt = {}) {
      let _date = new Date(),
        expires = "",
        _domain = opt.domain,
        _path = opt.path || "/",
        _time_gap = opt.time || 10 * 365 * 24 * 3600 * 1000;
      _date.setTime(_date.getTime() + _time_gap);
  
      if (!opt.sessionCookie) {
        expires = "; expires=" + _date.toUTCString()
      }
  
      document.cookie = key + "=" + value + "; path=" + _path + "; domain=" + _domain + expires
    },
    del: function (key, opt) {
      opt = opt || {};
      opt.time = -new Date();
      this.set(key, "", opt);
    }
  }
```

