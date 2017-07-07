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
