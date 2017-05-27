# Python Requests

### Add Header
```python
    Header = {'Content-Type':'application/x-www-form-urlencoded;                   charset=UTF-8'}
    rdata = {}
    Cookies = []
    res = request.post(url,headers=Header,data=rdata,cookies=Cookies)
#  print(json.dumps(res.json()["data"], indent = 4, sort_keys = True))
```


