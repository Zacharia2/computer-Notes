[TOC]


# 判断是文件还是文件夹

```js
//同步
const fs = require('fs');
var pathName = "E:image"
var stat = fs.lstatSync(pathName);
console.log(JSON.stringify(stat))
console.log('是否是文件：' + stat.isFile()) //是文件吗
console.log('是否是文件夹：' + stat.isDirectory()) //是文件夹吗
```

```js
//异步
const fs = require('fs');
var pathName = "E:image"
fs.stat(pathName, function (err, data) {
    console.log('是否是文件：' + data.isFile()) //是文件吗
    console.log('是否是文件夹：' + data.isDirectory()) //是文件夹吗
});
```

  

# 创建文件夹

```js
// 同步
const fs = window.require('fs'); // 引入文件系统模块
const { app } = window.require("electron").remote;
let mypath = app.getPath("documents") + "/space/";
if (!fs.existsSync(mypath)) {
    fs.mkdirSync(mypath);
}
```

```js
// 异步
const fs = window.require('fs'); // 引入文件系统模块
fs.mkdir(mypath, (err) => {
    if (err) throw err; // 如果出现错误就抛出错误信息
    console.log('文件夹创建成功');
});
```
  

## 创建多层目录


```js
//异步
const path = require("path");
const fs = require("fs");
let mypath = path.join(__dirname, "a", "b", "c", "d");
fs.mkdir(mypath, { recursive: true }, (err) => {
    if (err) throw err;
});
```

```js
//同步
const path = require("path");
const fs = require("fs");
let mypath = path.join(__dirname, "a", "b", "c", "d");
if (!fs.existsSync(mypath)) {
    fs.mkdirSync(mypath, { recursive: true });
}
```
  

# 获取文件所在文件夹

推荐方式

```js
const path = window.require("path");
const { app } = window.require("electron").remote;
let exepath = app.getPath("exe");
path.dirname(exepath);
// 或者
path.resolve(exepath, '..');
```
  


# 判断文件和文件夹是否存在


```js
//同步
if (!fs.existsSync(mypath)) {
    fs.mkdirSync(mypath);
}
```

```js
//异步
fs.exists("dirName", function (exists) {
    console.log(exists ? "创建成功" : "创建失败");
});
```

  

# 删除文件夹及文件

```js
var fs = require('fs'); // 引入fs模块

function deleteall(path) {
    var files = [];
    if (fs.existsSync(path)) {
        files = fs.readdirSync(path);
        files.forEach(function (file, index) {
            var curPath = path + "/" + file;
            if (fs.statSync(curPath).isDirectory()) { // recurse
                deleteall(curPath);
            } else { // delete file
                fs.unlinkSync(curPath);
            }
        });
        fs.rmdirSync(path);
    }
};
```

  

# 文件读取写入

## 创建文件

```js
fs.access(filename, fs.constants.F_OK, (err) => {
    if (!err) {
        fs.unlinkSync(filename);
    }
    fs.writeFile(filename, '', {
        'flag': 'a'
    }, function (err) {
        if (err) {
            throw err;
        }
    });
});
```
  

## 读取文件内容
```js
//同步读取
var fs = require("fs");
let mcontent = fs.readFileSync(filepath, "utf-8");
console.log(mcontent);
```

```js
//异步读取
var fs = require("fs");
fs.readFile(filepath, 'utf-8', function (err, data) {
    if (err) {
        console.log("error");
    } else {
        console.log(data);
    }
});
```
  

## 写入文件内容

### 同步写入


```js
fs.writeFileSync(filename, data, [options]);
```

```js
//示例
const fs = require('fs');
const content = '123456';
try {
    const data = fs.writeFileSync('/Users/me/test.txt', content);
} catch (err) {
    console.error(err);
}
```
  

默认情况下，此API将替换文件的内容（如果已经存在）。
您可以通过指定标志来修改默认值：
```js
fs.writeFile('/Users/me/test.txt', content, { flag: 'a+' }, (err) => { });
```

您可能会使用的标志是

- r+：打开文件进行读写
- w+：
	- 打开文件进行读写，将流放在文件的开头。 如果不存在则创建文件
	- 打开一个文件进行写入，将流放在文件末尾。 如果不存在则创建文件
- a+：打开文件进行读写，将流放在文件末尾。 如果不存在则创建文件


### 异步写入

```js
fs.writeFile(filename, data, [options], callback);
```

参数说明：

- filename:文件名
- data：需要写入的数据
- option：options参数值为一个对象,参数如下
	- flag属性：用于指定对该文件采取何种操作,默认值为’w’（文件不存在时创建该文件,文件已存在时重写该文件）,可指定值及其含义与readFile方法中使用的options参数值中的flag属性的可指定值及其含义相同。
	- mode属性：用于指定当文件被打开时对该文件的读写权限,默认值为0666（可读写）。该属性值及fs模块中的各方法中的mode参数值的指定方法均如下所示：使用4个数字组成mode属性值或?mode参数值,其中第一个数字必须是0,第二个 数字用于规定文件或目录所有者的权限,第三个数字用于规定文件或目录所有者所属用户组的权限,第四个数字规定其他人的权限。可以设定的数字如下所示：
		- 1：执行权限
		- 2：写权限
		- 4：读权限
	- encoding属性：用于指定使用何种编码格式来写入该文件。可指定属性值为“utf8”、“ascii”与“base64”。当data参数值为一个Buffer对象时该属性值被忽略,使用默认编码格式utf8来执行文件的写入。
- callback：回调函数

## 同步追加内容到文件底部

```js
fs.appendFileSync(filename, data, [options]);
```

  

## 异步追加内容到文件底部

```js
fs.appendFile(filename, data, [options], callback);
```

  

# 文件流写入

```js
const fs = require('fs');
const writer = fs.createWriteStream('./a.txt', {
    flags: 'a', //如果要把内容追加到文件原有的内容的后面，则设置flags为'a',此时设置start无效
});

//写入数据到流
writer.write('，适合去郊游,', 'utf8');
//再次向文件写入数据，会从当前位置开始写入
writer.write('咱们出发把！', 'utf8');
//关闭写入流，表明已没有数据要被写入可写流
writer.end()

writer.on('open', () => {
    console.log('文件已被打开', writer.pending);
});

writer.on('ready', () => {
    console.log('文件已为写入准备好', writer.pending);
});

writer.on('close', () => {
    console.log('文件已被关闭');
    console.log("总共写入了%d个字节", writer.bytesWritten);
    console.log('写入的文件路径是' + writer.path);
});
```
  

# 获取文件夹下文件


```js
const path = require("path");
const fs = require("fs");

let filepath_arr = [];
function mapDir(dir, containSonDir) {
    let files = fs.readdirSync(dir);
    files.forEach((filename) => {
        let pathname = path.join(dir, filename);
        let stats = fs.statSync(pathname);
        if (stats.isDirectory()) {
            if (containSonDir) {
                mapDir(pathname);
            }
        } else if (stats.isFile()) {
            let index = filename.lastIndexOf(".");
            //获取后缀
            let ext = filename.substr(index + 1);
            if (ext === "conf") {
                filepath_arr.push(pathname);
            }
        }
    });
}

function mapDirAll(dir, containSonDir) {
    filepath_arr = [];
    if (!containSonDir) {
        containSonDir = false;
    }
    return new Promise((resolve, reject) => {
        try {
            mapDir(dir, containSonDir);
        } catch (e) {
            reject(e);
        }
        resolve(filepath_arr);
    });
}

exports.mapDirAll = mapDirAll;
```
调用
```js
const { mapDirAll } = require("../utils/fileutil");
let basepath = "C:Users16798Documentsconf.d";
let stats = fs.statSync(basepath);
if (stats.isDirectory()) {
    let filepath_arr = await mapDirAll(basepath, false);
    console.info("filepath_arr:", filepath_arr);
}
```
  

# 路径操作

## 获取路径文件名

>` path.basename(path[, ext])`
> 获取路径中的文件名+文件扩展名
> 如果设置第二个参数表示过滤“.扩展名”，只要文件名称

```js
//示例：
const path = require('path');
var parseUrl = path.parse(url);
var basename1 = path.basename('/news/beijing/focus.html');
// 返回: 'focus.html'
console.log(basename1);
var basename2 = path.basename('/news/beijing/focus.htmll', '.html');
console.log(basename2);
//focus
```
  

## 获取路径中目录名

path.dirname() 方法返回 path 的目录名，类似于 Unix 的 dirname 命令。 尾部的目录分隔符将被忽略，参阅 path.sep。
```js
var parseUrl = path.parse(url);
path.dirname('/foo/bar/baz/asdf/a.exe');
// 返回: '/foo/bar/baz/asdf'
```
  

## 路径分割符

path.sep 路径分割符，提供平台特定的路径片段分隔符：
Windows 上是`\` ，POSIX 上是`/`。


```js
//例如，在 POSIX 上：
var parseUrl = path.parse(url);
'foo/bar/baz'.split(path.sep);
// 返回: ['foo', 'bar', 'baz']


//在 Windows 上：
'foobarbaz'.split(path.sep);
// 返回: ['foo', 'bar', 'baz']
```
  

## 获取当前文件的 根目录

```js
global.appRoot = path.resolve(__dirname);
//C:UsersThinkPadDesktopwebnode
```
注意：`__dirname` 当前目录  `__filename` 当前文件绝对路径


# 文件重命名

```js
// 同步
const fs = window.require("fs");
fs.renameSync(new_file_path, old_file_path);
```

```js
// 异步
const fs = window.require("fs");
fs.rename('sample.txt', 'sample_old.txt', function (err) {
    if (err) throw err;
    console.log('File Renamed.');
});
```