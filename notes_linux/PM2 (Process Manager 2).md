
https://blog.csdn.net/qq_36850813/article/details/98967807

## 启动服务
```sh
pm2 start app.js                //启动app.js应用
pm2 start app.js --name demo    //启动应用并设置name
pm2 start app.sh                //脚本启动
```

## 查看启动列表
```sh
pm2 list
```

## 重新启动
```sh
pm2 restart app.js        //同时杀死并重启所有进程。短时间内服务不可用。生成环境推荐使用reload
```

## 停止服务
```sh
pm2 stop all               //停止所有应用
pm2 stop [AppName]        //根据应用名停止指定应用
pm2 stop [ID]             //根据应用id停止指定应用
```

## 删除应用

```sh
pm2 delete all               //关闭并删除应用
pm2 delete [AppName]        //根据应用名关闭并删除应用
pm2 delete [ID]            //根据应用ID关闭并删除应用
```