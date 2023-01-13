```js
<script type="module">
        window.onload = function () {
            function Dimensions() //函数：获取尺寸
            {
                var winHeight;
                var height;
                //获取窗口高度
                if (window.innerHeight)
                    height = window.innerHeight;
                else if ((document.body) && (document.body.clientHeight))
                    height = document.body.clientHeight;
                winHeight = height - 16 + 'px';
                console.trace("result:" + winHeight)
                document.getElementById("aside-000").style.height = winHeight;//某元素id为aside-000。修改它的高度为浏览器窗口高度。
            }
            window.onresize = function () {
                window.location.reload();
                Dimensions();//窗口改变执行函数
            }
            Dimensions();//打开页面先进行函数执行
        }

    </script>
```