# 项目规范

## 目录

* [文件顶部规范](#rule)
* [请求与处理规范](#request)
* [文档注释规范](#doc)
* [分支规范](#branch)

#### <a name="rule">文件顶部规范</a>

在组件文件内顶部，应以以下顺序来加载`公共三方框架 > 公共三方工具 > 公共二方库 > 公共二方工具 > 公共一方依赖 > 私有依赖 > 全局变量定义`.

#### <a name="request">请求与处理规范</a>

**统一的请求API**： 通过`request.js`提供最后的发送动作，这里不处理任何业务逻辑与数据处理，单纯对发送前的参数做一些兜底(例如添加默认头部和一些默认参数的deep merge)和统一返回响应处理。
目前request动作是基于`fetch`API进行封装的，如果需要提供传输状态的事件响应(例如上传和下载)等复杂场景的请求，则可以另外使用自己的请求文件。

**统一的返回处理**：包括根据`Content-Type`对响应内容进行类型转化和根据`status code`的进行一些统一的客户端错误和服务端错误提示。并通过`Promise`将错误信息向上传递。

**各个业务模块负责好自己的中转层**：中专层主要是提供特定的接口调用API，比如获取列表的接口，中专层的文件包含这个业务模块的定制请求中间层和各个调用这个中间层API的请求API。目前在项目react项目中，还包含了actions内的一些动作。示例如下：
```javascript
const request = require('../utils/request'); // 统一的请求API

// 一些请求定制参数
const DEFAULT_HEADER = {
  'token-or-sth': 'Qddf33fdCD',
  'Content-Type': 'application/json; charset=UTF-8'
};
const METHODS = {
  GET: 'GET',
  POST: 'POST',
  PUT: 'PUT',
  DELETE: 'DELETE',
};

// 添加特殊的路由前缀到请求的链接
const fetchWithOptions = function (...args) {
  const url = `${your_module_api_prefix}${args[0]}`;
  const options = {
    headers: DEFAULT_HEADER,
    method: args[1],
  };

  if (args[2]) {
    options['body'] = JSON.stringify(args[2]);
  }

  return request(url, options);
};

// 输出请求参数，例如这个请求列表
export function fetchList(params) {
  // 提供一定程度的数据类型转化，但不直接处理业务逻辑
  const paramsString = util.transferObjToUrl(params);

  // 结合redux的例子，不用redux也可以准守这个规则
  return dispatch => fetchWithOptions(`${requestMaps.fetchList(params.tenantId)}?${paramsString}`, METHODS.GET, '')
    .then((data) => dispatch({ type: SUCCESS, data }))
    .catch(error => Promise.reject(error))
}
```

#### <a name="doc">文档注释规范</a>
请参考[jsDoc](http://usejsdoc.org/index.html)

#### <a name="branch">分支规范</a>
目前的建议是：**feature/{项目名}\_{年月日}\_{时间戳}**
详情请戳[关于分支污染的一次总结](https://wiki.sankuai.com/pages/viewpage.action?pageId=1016862517)
