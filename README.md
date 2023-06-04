
#### 方法二：GitHub Actions 运行

1. 登录[腾讯云后台](https://console.cloud.tencent.com/cam/capi)或者[阿里云后台](https://help.aliyun.com/document_detail/53045.html?spm=a2c4g.11186623.2.11.2c6a2fbdh13O53),获取 SecretId、SecretKey，如果使用阿里云DNS，注意需要添加DNS控制权限**AliyunDNSFullAccess**

2. Fork本项目到自己的仓库![fork.png](https://img.hostmonit.com/images/2020/11/05/fork.png)

3. 进入第二步中Fork的项目，点击Settings->Secrets and variables-> Actions -> New repository secret，分别是DOMAINS，KEY，SECRETID，SECRETKEY。

   > - DOMAINS  需改域名信息，填写时注意不要有换行  例如：`{"hostmonit.com": {"@": ["CM","CU","CT"], "shop": ["CM", "CU", "CT"], "stock": ["CM","CU","CT"]},"4096.me": {"@": ["CM","CU","CT"], "vv":["CM","CU","CT"]}}`
   > - DOMAINSV6 如果需要更新AAA解析请增加此secrets，格式同DOMAINS。
   > - KEY      API密钥，从[商店](https://shop.hostmonit.com)购买KEY，也可以使用这个KEY `o1zrmHAF` ，区别是 `o1zrmHAF` 是历史优选的Cloudflare IP(也可以从这个[网站](https://stock.hostmonit.com/CloudFlareYes)查到IP的信息)，而购买的KEY是15分钟内获取到的对各运营商速度最优的的Cloudflare IP
   > - SECRETID  第一部中从[腾讯云后台](https://console.cloud.tencent.com/cam/capi)或者[阿里云后台](https://help.aliyun.com/document_detail/53045.html?spm=a2c4g.11186623.2.11.2c6a2fbdh13O53),获取到的 `SECRETID  `
   > - SECRETKEY  第一部中从[腾讯云后台](https://console.cloud.tencent.com/cam/capi)或者[阿里云后台](https://help.aliyun.com/document_detail/53045.html?spm=a2c4g.11186623.2.11.2c6a2fbdh13O53),获取到的 `SECRETKEY`

   ![secret.png](https://img.hostmonit.com/images/2023/03/04/actions.png)

4. 修改您项目中的 `cf2dns_actions.py`文件中的`AFFECT_NUM`和`DNS_SERVER`参数，继续修改`.github/workflows/run.yml` 文件，定时执行的时长(建议15分钟执行一次)，最后点击 `start commit` 提交即可在Actions中的build查看到执行情况，如果看到 `cf2dns` 执行日志中有 `CHANGE DNS SUCCESS` 详情输出，即表示运行成功。**需要注意观察下次定时是否能正确运行，有时候GitHub Actions 挺抽风的**

   ![modify.png](https://img.hostmonit.com/images/2020/11/05/modify.png)


   ![commit.png](https://img.hostmonit.com/images/2020/11/05/commit.png)

   

   ![build.png](https://img.hostmonit.com/images/2020/11/05/build.png)

### 免责声明

> 1.网络环境错综复杂，适合我的不一定适合你，所以尽量先尝试免费的KEY或者购买试用版的KEY
>
> 2.有什么问题和建议请提issue或者Email我，不接受谩骂、扯皮、吐槽
>
> 3.为什么收费？ 这个标价我也根本不指望赚钱，甚至不够我国内一台VDS的钱。
>
> ★ 如果当前DNSPod有移动、联通、电信线路的解析将会覆盖掉

