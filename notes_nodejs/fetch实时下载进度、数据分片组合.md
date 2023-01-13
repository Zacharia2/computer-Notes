核心API：response.body.getReader()

```javascript

let oldProgress = 0;
const url = 'http://127.0.0.1/test.txt';
fetch(url).then(async function (response) {
    // headers数据
    // for (const date of response.headers) {}

    // 若跨域请求，则获取不到文件字节长度。
    const filesize = +response.headers.get('content-length');
    // 已下载字节
    let LoadedLength = 0;
    // 核心函数
    const reader = response.body.getReader();
    // 分块存储
    const chunks = {};
    // 持续读取流
    while (true) {
        // 核心函数
        const { done, value } = await reader.read();
        if (done) break;

        // 保存分块数据 => {0:[Uint8Array]}
        chunks[LoadedLength] = value;

        // 已下载的字节
        LoadedLength += value.length;

        // 下载进度
        const progress = (LoadedLength / filesize) * 100;
        // 将跳跃式数值连续
        const timer = setInterval(function () {
            const number = oldProgress += 1;
            document.body.innerHTML = Math.floor(number) + '%';
            if (oldProgress >= progress) {
                oldProgress = progress;
                clearInterval(timer);
            }
        }, progress);

    }

    // 组合分块数据
    let chunksAll = new Uint8Array(LoadedLength);
    for (const index of Object.keys(chunks)) {
        // Uint8Array.prototype.set(数组,偏移值)
        chunksAll.set(chunks[index], index)
    }

    // 转码为字符串
    const textDecoder = new TextDecoder('gb2312');
    console.log(textDecoder.decode(chunksAll));

});
```