# JSBridge
JSBridge交接与Native通信是Web端调用进行封装,之前一直做移动web开发，项目需要webview+native的混合模式所以需要一些web和native的交互，由于JSBridge Native端作者提供web调用方式太奇怪，也跟web开发代码不耦合，所以我对web调用方式进行封装，针对IOS和Android做了兼容，方便在web开发时进行调用。

# 方法添加示例
```
JSBridge.prototype.getUserInfo = function(data, callback) {
        this._init(function(bridge) {
            this.__init__(bridge);
            bridge.callHandler('getUserInfo', data, function(response) {
                if(typeof response === 'object'){
                    callback(response)
                }else{
                    callback(JSON.parse(response));
                }
            })
        }.bind(this))
    };
```
这是在JSBridge.js中写的一个方法，当添加新方法的时候只需要在JSBridge.js中提示的位置复制上面代码，
修改JSBridge.prototype.getUserInfo为 JSBridge.prototype.yourMethod（例如JSBridge.prototype.setTitle等等）
修改bridge.callHandler的第一个参数（与Native端定义的方法名称）
# 注意事项

如果需要修改Native定义的路径，可以在JSBridge.js中JSBridge.prototype._init下
```
WVJBIframe.src = 'wvjbscheme://__BRIDGE_LOADED__';
```
JSBridge.prototype._init是初始化方法

JSBridge.prototype.\__init__ 这个安卓下必须调用，应该也是初始化的一部分（不懂原生的东西）

你也可以在Vue等框架下调用
```
import JSBridge from './JSBridge';
var JSBridge = require('./JSBridge')
```
Vue我比较熟悉，可以单独写个插件利用Vue.use挂载到实例上这样在任何组件都能调用
