## AutoBuy 自动售卖系统

## 安装步骤

首先，将程序克隆到本地：

```
git clone https://github.com/Qsnh/AutoBuy.git
```

安装依赖：

```
composer install
```

复制 `.env` ：

```
cp .env.example .env
```

在 `.env` 环境中配置好数据库等信息。执行：

```
php artisan key:generate
```

设置 `storage` 目录权限：

```
sudo chmod -R 0777 storage
```

安装数据库表：

```
php artisan migrate
```

填充默认数据：

```
php artisan db:seed
```

到这里安装结束。
  
后台地址：http://domain.app/home  
管理员账号密码：  

```
username: auto_buy@admin.com
password: admin123
```

> 如果想要程序完整的运行，还需要进行下面的配置。

## 其它配置

#### 支付配置 

本套系统的支付解决方式来自这一篇文章：[基于有赞云的个人收款即时到帐实现方案](https://laravel-china.org/articles/7014/real-time-account-implementation-scheme-based-on-personal-receipts-with-praise-clouds),您在阅读了上面的文章之后，请配置下 `.env` 文件中的：

```
YOUZAN_CLIENT_ID=
YOUZAN_CLIENT_SECRET=
YOUZAN_KDT_ID=
```

#### 邮箱配置

请参考：[http://www.cnblogs.com/taotaoxixihaha/p/6650845.html](http://www.cnblogs.com/taotaoxixihaha/p/6650845.html)

#### 定时任务配置

请参考：[https://laravel.com/docs/5.5/scheduling](https://laravel.com/docs/5.5/scheduling)

#### 备份文件云存储

这里如果我想要将备份的文件存储到七牛云我应该这样配置，修改 `.env` 文件：

```
BACKUP_SAVE_DISK=qiniu

QINIU_DOMAIN=https://qiniu.com(示例)
QINIU_ACCESS_KEY=1
QINIU_SECRET_KEY=2
QINIU_BUCKET=3
```

#### 备份结果通知

```
BACKUP_NOTIFICATION_EMAIL=youemail@email.com
```

> 前提必须要配置好邮箱配置！！！

## 扩展包

| 扩展包 | 描述 | 应用场景 |
| --- | --- | --- |
| [laracasts/flash](https://github.com/laracasts/flash) | 验证消息，通知消息输出 | 用于表单验证，业务逻辑验证等 |
| [mewebstudio/captcha](https://github.com/mewebstudio/captcha) | 图形验证码 | 图形验证码 |
| [overtrue/laravel-youzan](https://github.com/overtrue/laravel-youzan) | 基于laravel封装的有赞扩展包 | 个人收款解决方案 |
| [rap2hpoutre/laravel-log-viewer](https://github.com/rap2hpoutre/laravel-log-viewer) | laravel日志查看 | laravel日志查看 |
| [yangyifan/upload](https://github.com/yangyifan/upload) | laravel filesystem扩展包 | 七牛，又拍，阿里云，腾讯云等存储服务 |
| [spatie/laravel-backup](https://github.com/spatie/laravel-backup) | 数据备份 | 网站备份，数据库定时备份等 |

## 自定义命令

| 命令 | 描述 |
| --- | --- |
| `password:reset` | 重置管理员密码 |
| `order:query` | 查询最近5条未支付订单的支付情况 |
| `backup:run` | 备份当前网站 |

## 定时任务

| 任务 | 描述 | 周期 |
| --- | --- | --- |
| `order:query` | 查询最近5条(循环重置)未支付订单的支付情况 | 每分钟 |
| `backup:run` | 备份当前网站 | 每天凌晨3:00 |
| `backup:clear` | 清除过期备份 | 每天凌晨4:00 |


## 作者

[轻色年华](https://github.com/Qsnh)

## License

MIT

