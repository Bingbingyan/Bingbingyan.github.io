# 目录结构
## ng-if
``` html
<div ng-if="par > 1">  display </div>
```
``` javascript
$scope.par = 0
```

## ng-model
将数据双向绑定到页面上，当页面发生修改时，js 能够同步处理变更的值。


## ng-class
```html
<div ng-class="par=='a'?'btn btn-default':'btn btn-warning'">
```
- 当 par == ‘a’ 时，Element class 使用‘btn-default’


## ng-enable & ng-disable
- 同 ng-class


## ng-repeat
```html
<div ng-repeat="device in app.deviceList " >
```



