# express-convert

> Convert express middleware to koa middleware  
> There is some difference between Express middleware and the converter, please see below.

## Install
```
npm install express-convert
```

## Usage
```javascript
const convert = require('express-convert');
const Koa = require('koa');
const app = new Koa();

app.use(convert(expressMiddleware));
```

## Express Compatibility

| express-convert | express |
| --------------- | ------- |
| `@1`            | `@4`    |

## Feature

| Version |   `res.jsonp()`    | Custom JSON parser** |
| :-----: | :----------------: | :------------------: |
|  1.2.0  |        :x:         |         :x:          |
|  1.3.0  |     :o:**\***      |         :x:          |
|  1.3.1  | :heavy_check_mark: |         :x:          |
|  1.4.0  | :heavy_check_mark: |  :heavy_check_mark:  |

\* does not support custom callback name  
\*\* the custom parser only applies on the `res.jsonp()` method because Koa will parse JSON for you in other cases.

## Some differences

- `req.app`: req.app is a `Koa` app instance, not an `Express` app instance.
- Application Setting: The only setting implemented now is `jsonp callback name` for `res.jsonp()`.
- `req.cookies`: Koa uses the `cookies` module so this property is not a parsed cookie object, for what it is, see [Koa documents](https://koajs.com/#context).
- `req.params`, `req.app.METHOD()` and `req.route`: Koa does not have router, so the properties is always `undefined` and the method always returns `undefined` and do nothing.
- `req.signedCookies`: this property is `undefined`, use `req.cookies.get()` with `signed` option.
- `req.range()`: Koa dones't support this, so this function always return undefined and do nothing.
- `res.locals`: Koa dones't support this, so this would be a empty object.
- `res.cookie`: Koa uses the `cookie` module to do the job, so the option is a little bit different, for more information, see [Koa documents](https://koajs.com/#context).
- `res.clearCookie()`: Koa does not support it, so this function will always return undefined and do nothing.
- `res.download()` and `res.sendFile()`: Koa does not support it, so this function will always return undefined and do nothing, consider use `res.attach()` to do file hosting job.
- `res.end()`: This generally does nothing because in Koa you do not need to end the response manually, just do nothing. Koa will end the response automatically.
- `res.jsonp()`: Koa does not have integrated support for this method, this is only a simple implementation. For better jsonp support, have a look at [koa-jsonp](https://github.com/kilianc/koa-jsonp).
- `res.location()` and `res.links()`: Koa does not have integrated support for them, but I plan to implement them in future versions, now they generally do nothing.
- `res.render()`: Koa does not support this, so it does nothing.
