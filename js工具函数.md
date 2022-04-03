### 操作localStorage

```js
//sto
export const setStore = (name, content) => {
	if (!name) return;
	if (typeof content !== "string") {
		content = JSON.stringify(content);
	}
	window.localStorage.setItem(name, content);
};
export const getStore = (name) => {
	if (!name) return;
	return window.localStorage.getItem(name);
};
export const removeStore = (name) => {
	if (!name) return;
	window.localStorage.removeItem(name);
};

```



### 生成随机数

```js
function RADOM(max, min) {
	return Math.random() * (max - min) + min;
}
```

## 数组操作

### 数组扁平化

```js
function flatten(arr) {
	let result = [];
	for (let i = 0; i < arr.length; i++) {
		if (Array.isArray(arr[i])) {
			result = result.concat(flatten(arr[i]));
		} else {
			result.push(arr[i]);
		}
	}
	return result;
}
```

## 字符串操作

### 字符串首字母大写

```js
function firstLetterUpper(str) {
	return str.charAt(0).toUpperCase() + str.slice(1);
}
```

### 手机号中间四位变成*

```js
function telFormat(tel) {
	tel = String(tel);
	return tel.substr(0, 3) + "****" + tel.substr(7);
}
```

### 驼峰命名转换成短横线命名

```js
function getKebabCase(str) {
	return str.replace(/[A-Z]/g, (item) => "-" + item.toLowerCase());
}
```

### 短横线命名转换成驼峰命名

```js
function getCamelCase(str) {
	return str.replace(/-([a-z])/g, (i, item) => item.toUpperCase());
}
```

### 操作cookie

### 设置cookie

```js
export const setCookie = (key, value, expire) => {
    const d = new Date();
    d.setDate(d.getDate() + expire);
    document.cookie = `${key}=${value};expires=${d.toUTCString()}`
};
```

### 读取cookie

```js
export const getCookie = (key) => {
    const cookieStr = unescape(document.cookie);
       const arr = cookieStr.split('; ');
       let cookieValue = '';
       for (let i = 0; i < arr.length; i++) {
           const temp = arr[i].split('=');
           if (temp[0] === key) {
               cookieValue = temp[1];
               break
       }
    }
    return cookieValue
};
```

### 删除cookie

## 操作url

### 获取URL参数列表

```js
export const GetRequest = () => {
    let url = location.search;
    const paramsStr = /.+\?(.+)$/.exec(url)[1]; // 将 ? 后面的字符串取出来
    const paramsArr = paramsStr.split('&'); // 将字符串以 & 分割后存到数组中
    let paramsObj = {};
    // 将 params 存到对象中
    paramsArr.forEach(param => {
      if (/=/.test(param)) { // 处理有 value 的参数
        let [key, val] = param.split('='); // 分割 key 和 value
        val = decodeURIComponent(val); // 解码
        val = /^\d+$/.test(val) ? parseFloat(val) : val; // 判断是否转为数字
        if (paramsObj.hasOwnProperty(key)) { // 如果对象有 key，则添加一个值
          paramsObj[key] = [].concat(paramsObj[key], val);
        } else { // 如果对象没有这个 key，创建 key 并设置值
          paramsObj[key] = val;
        }
      } else { // 处理没有 value 的参数
        paramsObj[param] = true;
      }
    })
    return paramsObj;
};
```



### 检测URL是否有效

```js
export const getUrlState = (URL) => {
  let xmlhttp = new ActiveXObject("microsoft.xmlhttp");
  xmlhttp.Open("GET", URL, false);
  try {
    xmlhttp.Send();
  } catch (e) {
  } finally {
    let result = xmlhttp.responseText;
    if (result) {
      if (xmlhttp.Status == 200) {
        return true;
      } else {
        return false;
      }
    } else {
      return false;
    }
  }
}
```

### 获取

## 浏览器操作url参数

使用正则表达式获取url:

```js
function getParams(url, params){
      var res = new RegExp("(?:&|/?)" + params + "=([^&$]+)").exec(url);
      return res ? res[1] : '';
}

// url: xx.com?id=2&isShare=true
const id = getParams(window.location.search, 'id')

console.log(id) // 2
```

使用URLSearchParams获取url参数

```js
const urlSearchParams = new URLSearchParams(window.location.search);
const params = Object.fromEntries(urlSearchParams.entries());

console.log(params) // {id: '2', isShare: 'true'}
console.log(params.id) // 2
```



### 滚动到页面顶部

``` js
export const scrollToTop = () => {
  const height = document.documentElement.scrollTop || document.body.scrollTop;
  if (height > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, height - height / 8);
  }
}
```

### 滚动到页面底部

```js
export const scrollToBottom = () => {
  window.scrollTo(0, document.documentElement.clientHeight);  
}
```

### 滚动到指定元素区域

```js
export const smoothScroll = (element) => {
    document.querySelector(element).scrollIntoView({
        behavior: 'smooth'
    });
};
```

### 打开浏览器全屏

```js
export const toFullScreen = () => {
    let element = document.body;
    if (element.requestFullscreen) {
      element.requestFullscreen()
    } else if (element.mozRequestFullScreen) {
      element.mozRequestFullScreen()
    } else if (element.msRequestFullscreen) {
      element.msRequestFullscreen()
    } else if (element.webkitRequestFullscreen) {
      element.webkitRequestFullScreen()
    }
}
```

