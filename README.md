## 实现功能

- [x] CNNVD漏洞实时监控
- [x] CVE漏洞实时监控
- [x] 漏洞预警
- [x] 第三方依赖分析

## 安装使用

### 后端

**安装第三方库**

```
pip3 install -r requirements.txt
```

**设置数据库**

在主目录下settings.py，修改数据库配置信息

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7u9o1nw6cj30kk07nmxk.jpg)

**创建数据库表**

```
python3 manage.py makemigrations
python3 manage.py migrate
```

**定时启动任务**

settings.py部署定时任务，时间间隔可修改

```
CRONJOBS = (
    ('* */3 * * *', 'apps.cnnvd.crontab.cnnvdCrontab', ' >> /root/Eye/scheduled_job.log '),
    ('* */3 * * *', 'apps.cve.crontab.cveCrontab', ' >> /root/Eye/scheduled_job.log '),
    ('* */3 * * *', 'apps.aliyun.crontab.aliyunCrontab', ' >> /root/Eye/scheduled_job.log '),
)
```

Linux定时启动

```
# 添加、修改任务
python3 manage.py crontab add
# 显示当前的定时任务 
python3 manage.py crontab show
# 如果要移除所有的任务
python3 manage.py crontab remove

```

**第一次启动可先获取数据**

脚本里可分别CNNVD、CVE、漏洞预警相关信息(可自行配置)

```
python3 real_time_scrape.py
```

**启动运行**

```
python3 manage.py runserver 8888
```

### 前端

```
npm install
npm start
```

## 效果展示

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7ua9dj4anj31780u0dpe.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7ua38jmjfj30sc0h2dhg.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7ua3umh0dj30ob0humyi.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7ua48oxkej310k0ifdi3.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7ub2xkgntj30uk0kqdj4.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g7uaaylgbtj30u60jdtb2.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g8lb61niz9j318f0u0tfh.jpg)

![](https://tva1.sinaimg.cn/large/006y8mN6ly1g8lb82qthij31lx0u0akc.jpg)
