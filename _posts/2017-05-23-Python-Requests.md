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

res = requests.post(url, data=json.dumps(data), headers=headers)
# json = data 不需要设置 Content-Type = json 的 Header
res = requests.post(url, json=data)


```

