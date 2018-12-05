# Gzip
Gzip 压缩 解压


byteToString: function(arr) {
    if (typeof arr === 'string') {
        return arr;
    }
    var str = '',
        _arr = arr;
    for (var i = 0; i < _arr.length; i++) {
        var one = _arr[i].toString(2),
            v = one.match(/^1+?(?=0)/);
        if (v && one.length == 8) {
            var bytesLength = v[0].length;
            var store = _arr[i].toString(2).slice(7 - bytesLength);
            for (var st = 1; st < bytesLength; st++) {
                store += _arr[st + i].toString(2).slice(2);
            }
            str += String.fromCharCode(parseInt(store, 2));
            i += bytesLength - 1;
        } else {
            str += String.fromCharCode(_arr[i]);
        }
    }
    return str;
},

使用 示例：
var pako = require('pako.js');
var compressByteArray = new Uint8Array(strArr);


var data = pako.inflate(compressByteArray);

// 将GunZip ByTAREAR转换回ASCII字符串
var str = String.fromCharCode.apply(null, new Uint16Array(data));
cc.log("str    ", str);
// 将GunZip ByTAREAR转换回Utf-8字符串
var str = this.byteToString(data);  //  上面 函数 已给出
cc.log("str    ", str);
测试 输出 数据
str     {"data":{"channelType":1,"head":"500001","level":3,"msg":"fasdfa","nickname":"ä¸å®å®å®","senderId":28,"time":1543974120817},"main":0,"sub":0}
wbSocket.js:112 str {"data":{"channelType":1,"head":"500001","level":3,"msg":"fasdfa","nickname":"上官安安","senderId":28,"time":1543974120817},"main":0,"sub":0}
