# Python Requests

### Add Header

```python
    Header = {'Content-Type':'application/x-www-form-urlencoded;                   charset=UTF-8'}
    rdata = {}
    Cookies = []
    res = request.post(url,headers=Header,data=rdata,cookies=Cookies)
#  print(json.dumps(res.json()["data"], indent = 4, sort_keys = True))
```

### Request json 与 data 区别

```python
headers = {"Content-Type": "application/json;charset=UTF-8",
"Accept": "application/json, text/plain, */*",
"User-Agen": agent }

# 需要设置 Header
res = requests.post(url, data=json.dumps(data), headers=headers)
# json = data 不需要设置 Content-Type = json 的 Header
res = requests.post(url, json=data)


```
### format Json 不将中文转换编码格式
```python
print(json.dumps(queryJson, indent = 4, ensure_ascii = False))
```

### https request
```python
import requests
import requests.packages.urllib3.util.ssl_
requests.packages.urllib3.util.ssl_.DEFAULT_CIPHERS = 'ALL'
res = request.get("https://www.xxx.com")
```

### 自定义排序规则

```python
from collections import OrderedDict
sort_order = ['@name', '#text']
items_orderd = [OrderedDict(sorted(item.iteritems(), key=lambda (k, v): sort_order.index(k)))
                    for item in items]
```

作者：Python 程序员
链接：https://zhuanlan.zhihu.com/p/28920257
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

1、概览 1.1、实例引入# 引入 Requests 库
import requests

# 发起 GET 请求
response = requests.get('https://www.baidu.com/')
# 查看响应类型  requests.models.Response
print(type(response))
# 输出状态码
print(response.status_code)
# 输出响应内容类型  text
print(type(response.text))
# 输出响应内容
print(response.text)
# 输出 cookies
print(response.cookies)
1.2、各种请求方式 import requests

# 发起 POST 请求
requests.post('http://httpbin.org/post')
# 发起 PUT 请求
requests.put('http://httpbin.org/put')
# 发起 DELETE 请求
requests.delete('http://httpbin.org/delete')
# 发送 HEAD 请求
requests.head('http://httpbin.org/get')
# 发送 OPTION 请求
requests.options('http://httpbin.org/get')
2、请求 2.1 、基本 GET 请求 2.1.1、基本写法 import requests

response = requests.get('http://httpbin.org/get')
print(response.text)
2.1.2、带参数的 GET 请求 import requests

response = requests.get('http://httpbin.org/get?name=jyx&age=18')
print(response.text)
2.1.3、带参数的 GET 请求 (2)import requests

# 分装 GET 请求参数
param = {'name':'jyx','age':19}
# 设置 GET 请求参数 (Params)
response = requests.get('http://httpbin.org/get',params=param)
print(response.text)
2.1.4、解析 jsonimport requests

response = requests.get('http://httpbin.org/get')
# 获取响应内容
print(type(response.text))
# 如果响应内容是 json, 就将其转为 json
print(response.json())
# 输出的是字典类型
print(type(response.json()))
2.1.5、获取二进制数据 import requests

response = requests.get('http://github.com/favicon.ico')

# str，bytes
print(type(response.text),type(response.content))
# 输出响应的文本内容
print(response.text)
# 输出响应的二进制内容
print(response.content)
# 下载二进制数据到本地
with open('favicon.ico','wb') as f:
  f.write(response.content)
  f.close()
2.1.6、添加 headersimport requests

# 设置 User-Agent 浏览器信息
headers = {
      "User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.133 Safari/537.36"
}
# 设置请求头信息
response = requests.get('https://www.zhihu.com/explore',headers=headers)
print(response.text)
2.2、基本 POST 请求 import requests

# 设置传入 post 表单信息
data= { 'name':'jyx', 'age':18}
# 设置请求头信息
headers = {
      "User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.133 Safari/537.36"
}
# 设置请求头信息和 POST 请求参数 (data)
response = requests.post('http://httpbin.org/post', data=data, headers=headers)
print(response.text)
3、响应 3.1 response 属性 import requests

response = requests.get('http://www.jianshu.com/')
# 获取响应状态码
print(type(response.status_code),response.status_code)
# 获取响应头信息
 print(type(response.headers),response.headers)
# 获取响应头中的 cookies
print(type(response.cookies),response.cookies)
# 获取访问的 url
 print(type(response.url),response.url)
# 获取访问的历史记录
 print(type(response.history),response.history)
3.2、 状态码判断 import requests

response = requests.get('http://www.jianshu.com/404.html')
# 使用 request 内置的字母判断状态码
if not response.status_code == requests.codes.ok:
    print('404-1')
response = requests.get('http://www.jianshu.com')
# 使用状态码数字判断
if not response.status_code == 200:
    print('404-2')
3.3 requests 内置的状态字符 100: ('continue',),   101: ('switching_protocols',),   102: ('processing',),   103: ('checkpoint',),   122: ('uri_too_long', 'request_uri_too_long'),   200: ('ok', 'okay', 'all_ok', 'all_okay', 'all_good', '\\o/', '✓'),   201: ('created',),   202: ('accepted',),   203: ('non_authoritative_info', 'non_authoritative_information'),   204: ('no_content',),   205: ('reset_content', 'reset'),   206: ('partial_content', 'partial'),   207: ('multi_status', 'multiple_status', 'multi_stati', 'multiple_stati'),   208: ('already_reported',),   226: ('im_used',),   # Redirection.   300: ('multiple_choices',),   301: ('moved_permanently', 'moved', '\\'),   302: ('found',),   303: ('see_other', 'other'),   304: ('not_modified',),   305: ('use_proxy',),   306: ('switch_proxy',),   307: ('temporary_redirect', 'temporary_moved', 'temporary'),   308: ('permanent_redirect', 'resume_incomplete', 'resume',), # These 2 to be removed in 3.0   # Client Error.   400: ('bad_request', 'bad'),   401: ('unauthorized',),   402: ('payment_required', 'payment'),   403: ('forbidden',),   404: ('not_found', '-'),   405: ('method_not_allowed', 'not_allowed'),   406: ('not_acceptable',),   407: ('proxy_authentication_required', 'proxy_auth', 'proxy_authentication'),   408: ('request_timeout', 'timeout'),   409: ('conflict',),   410: ('gone',),   411: ('length_required',),   412: ('precondition_failed', 'precondition'),   413: ('request_entity_too_large',),   414: ('request_uri_too_large',),   415: ('unsupported_media_type', 'unsupported_media', 'media_type'),   416: ('requested_range_not_satisfiable', 'requested_range', 'range_not_satisfiable'),   417: ('expectation_failed',),   418: ('im_a_teapot', 'teapot', 'i_am_a_teapot'),   421: ('misdirected_request',),   422: ('unprocessable_entity', 'unprocessable'),   423: ('locked',),   424: ('failed_dependency', 'dependency'),   425: ('unordered_collection', 'unordered'),   426: ('upgrade_required', 'upgrade'),   428: ('precondition_required', 'precondition'),   429: ('too_many_requests', 'too_many'),   431: ('header_fields_too_large', 'fields_too_large'),   444: ('no_response', 'none'),   449: ('retry_with', 'retry'),   450: ('blocked_by_windows_parental_controls', 'parental_controls'),   451: ('unavailable_for_legal_reasons', 'legal_reasons'),   499: ('client_closed_request',),   # Server Error.   500: ('internal_server_error', 'server_error', '/o\\', '✗'),   501: ('not_implemented',),   502: ('bad_gateway',),   503: ('service_unavailable', 'unavailable'),   504: ('gateway_timeout',),   505: ('http_version_not_supported', 'http_version'),   506: ('variant_also_negotiates',),   507: ('insufficient_storage',),   509: ('bandwidth_limit_exceeded', 'bandwidth'),   510: ('not_extended',),   511: ('network_authentication_required', 'network_auth', 'network_authentication'),4、高级操作 4.1、文件上传 import requests

files = {'file':open('favicon.ico','rb')}
# 往 POST 请求头中设置文件 (files)
response = requests.post('http://httpbin.org/post',files=files)
print(response.text)
4.2、获取 cookiesimport requests

response = requests.get('https://www.baidu.com')
print(response.cookies)
for key,value in response.cookies.items():
    print(key,'=====',value)
4.3、会话维持 4.3.1、普通请求 import requests

requests.get('http://httpbin.org/cookies/set/number/12456')
response = requests.get('http://httpbin.org/cookies')
# 本质上是两次不同的请求，session 不一致
print(response.text)
4.3.2、会话维持请求 import requests

# 从 Requests 中获取 session
session = requests.session()
# 使用 seesion 去请求保证了请求是同一个 session
session.get('http://httpbin.org/cookies/set/number/12456')
response = session.get('http://httpbin.org/cookies')
print(response.text)
4.4、证书验证 4.4.1、无证书访问 import requests

response = requests.get('https://www.12306.cn')
# 在请求 https 时，request 会进行证书的验证，如果验证失败则会抛出异常
print(response.status_code)
4.4.2、关闭证书验证 import requests

# 关闭验证，但是仍然会报出证书警告
response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
4.4.3、消除关闭证书验证的警告 from requests.packages import urllib3
import requests

# 关闭警告
urllib3.disable_warnings()
response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
4.4.4、手动设置证书 import requests

# 设置本地证书
response = requests.get('https://www.12306.cn', cert=('/path/server.crt', '/path/key'))
print(response.status_code)
4.5、代理设置 4.5.1、设置普通代理 import requests

proxies = {
    "http": "http://127.0.0.1:9743",
    "https": "https://127.0.0.1:9743",
}
# 往请求中设置代理 (proxies
)
response = requests.get("https://www.taobao.com", proxies=proxies)
print(response.status_code)
4.5.2、设置带有用户名和密码的代理 import requests

proxies = {
    "http": "http://user:password@127.0.0.1:9743/",
}
response = requests.get("https://www.taobao.com", proxies=proxies)
print(response.status_code)
4.5.3、设置 socks 代理 pip3 install 'requests[socks] import requests

proxies = {
    'http': 'socks5://127.0.0.1:9742',
    'https': 'socks5://127.0.0.1:9742'
}
response = requests.get("https://www.taobao.com", proxies=proxies)
print(response.status_code)
4.6、超时设置 import requests
from requests.exceptions import ReadTimeout



try:
   # 设置必须在 500ms 内收到响应，不然或抛出 ReadTimeout 异常
   response = requests.get("http://httpbin.org/get", timeout=0.5)
            print(response.status_code)
except ReadTimeout:
   print('Timeout')
4.7、认证设置 import requests
from requests.auth import HTTPBasicAuth

r = requests.get('http://120.27.34.24:9001', auth=HTTPBasicAuth('user', '123'))
# r = requests.get('http://120.27.34.24:9001', auth=('user', '123'))
print(r.status_code)
4.8、异常处理 import requests
from requests.exceptions import ReadTimeout, ConnectionError, RequestException

try:
   response = requests.get("http://httpbin.org/get", timeout = 0.5)
           print(response.status_code)
except ReadTimeout:
   # 超时异常
   print('Timeout')
except ConnectionError:
   # 连接异常
   print('Connection error')
except RequestException:
   # 请求异常
   print('Error')
作者：蒋蜀黍  Python 爱好者社区专栏作者   授权原创发布，请勿转载，谢谢。出处：Requests 库学习笔记推荐免费视频教程：Python3 爬虫三大案例实战分享：猫眼电影、今日头条街拍美图、淘宝美食 Python3 爬虫三大案例实战分享公众号：Python 爱好者社区（微信 ID：python_shequ）小编个人微信：tsdatajob ，来不急回复的，可以加小编微信沟通，谢谢。
