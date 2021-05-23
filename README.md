# v2rayN
## 一、最新版V2RayN客户端下载
软件下载地址：https://github.com/2dust/v2rayN/tags 
## 二、系统代理
- 清除系统代理（禁用代理）：
        意思是清空/禁用Windows系列“网络和Internet”-“代理”中的代理设置。
- 自动配置系统代理（全局代理）：
       意思是自动填入Windows系列“网络和Internet”-“代理”中的代理配置。
- 不改变系统代理（保持系统代理）：
       意思是不对Windows系列“网络和Internet”-“代理”中的代理配置进行修改。
       
    经过实际测试，会发现 “自动配置系统代理”和? “不改变系统代理”，都是全局代理，也就是所有连接都通过代理。
## 三、 参数设置
点击V2RayN界面“设置”-“参数设置”-“V2RayN设置”，勾选“更新Core时忽略Geo文件”，Core类型选"Xray_core"
## 四、 基础规则
- 基础规则——一键导入基础规则 

### Proxy (代理)、Direct (直连)、Block (阻止)的含义
- Block (阻止)： 拦截向外发送的连接请求，禁止连网。 
- Direct (直连)： 直接访问外部网络，不走代理。
- Proxy (代理)： 允许通过代理连接上网。
## 五、 V2RayN高级路由器配置规则集
- GFWlist黑名单（PAC代理模式）
- Whitelist白名单（绕过大陆模式）
- 全局代理
- 全局直连
- 全局阻断
直接将本文的规则代码，复制、导入到电脑客户端V2RayN内即可使用，导入教程请参考《一分钟设置V2rayN路由方法》：https://www.youtube.com/watch?v=HLNvXEzpgl8
### GFWlist黑名单（PAC代理模式）
    [
      {
    "outboundTag": "proxy",
    "domain": [
      "#以下三行是GitHub网站，为了不影响下载速度走代理",
      "github.com",
      "githubassets.com",
      "githubusercontent.com"
    ]
    },
    {
    "outboundTag": "block",
    "domain": [
      "#阻止CrxMouse鼠标手势收集上网数据",
      "mousegesturesapi.com"
    ]
    },
    {
    "outboundTag": "direct",
    "domain": [
      "bitwarden.com",
      "bitwarden.net",
      "baiyunju.cc",
      "letsencrypt.org",
      "adblockplus.org",
      "safesugar.net",
      "#下两行谷歌广告",
      "googleads.g.doubleclick.net",
      "adservice.google.com",
      "#【以下全部是geo预定义域名列表】",
      "#下一行是所有私有域名",
      "geosite:private",
      "#下一行包含常见大陆站点域名和CNNIC管理的大陆域名，即geolocation-cn和tld-cn的合集",
      "geosite:cn",
      "#下一行包含所有Adobe旗下域名",
      "geosite:adobe",
      "#下一行包含所有Adobe正版激活域名",
      "geosite:adobe-activation",
      "#下一行包含所有微软旗下域名",
      "geosite:microsoft",
      "#下一行包含微软msn相关域名少数与上一行微软列表重复",
      "geosite:msn",
      "#下一行包含所有苹果旗下域名",
      "geosite:apple",
      "#下一行包含所有广告平台、提供商域名",
      "geosite:category-ads-all",
      "#下一行包含可直连访问谷歌网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:google-cn",
      "#下一行包含可直连访问苹果网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:apple-cn"
    ]
    },
    {
    "type": "field",
    "outboundTag": "proxy",
    "domain": [
      "#GFW域名列表",
      "geosite:gfw",
      "geosite:greatfire"
    ]
    },
    {
    "type": "field",
    "port": "0-65535",
    "outboundTag": "direct"
    }
    ]

### 说明：
- 上面V2Ray高级路由规则集，完美实现了PAC代理模式，效果完全一样。其原理是，GFW黑名单中的域名走代理，剩余的其他连接0-65535所有端口的所有国内、外网站流量全部直连。
- #号开头的为注释行，不必删除。
- 其中，第三行直连域名规则中的域名较多，其实这一行”direct”规则原本可以全部删掉，但是在使用中发现，有一些本来可以直连的域名，也被放入GFW列表中走代理了，为了避免有漏网域名没走直连，因此直接将之前基础路由功能中的直接域名列表复制过来，与后面两行规则并不冲突。

## Whitelist白名单（绕过大陆代理模式）
也就是CNNIC 管理的用于中国大陆的顶级域名，以及服务器位于中国内陆的IP，全部直连，其他所有网址代理。
不过，其中有一些可以连接没有被墙的国外网址，也放进了直连规则内，如果不需要可以自己修改。

    [
    {
    "port": "",
    "outboundTag": "proxy",
    "ip": [],
    "domain": [
      "#以下三行是GitHub网站，为了不影响下载速度走代理",
      "github.com",
      "githubassets.com",
      "githubusercontent.com"
      ],
      "protocol": []
      },
      {
    "type": "field",
    "outboundTag": "block",
    "domain": [
      "#阻止CrxMouse鼠标手势收集上网数据",
      "mousegesturesapi.com",
      "#下一行广告管理平台网址，在ProductivityTab（原iChrome）浏览器插件页面显示",
      "cf-se.com"
      ]
      },
      {
    "type": "field",
    "port": "",
    "outboundTag": "direct",
    "ip": [
      "geoip:private",
      "geoip:cn"
    ],
    "domain": [
      "bitwarden.com",
      "bitwarden.net",
      "gravatar.com",
      "gstatic.com",
      "baiyunju.cc",
      "letsencrypt.org",
      "adblockplus.org",
      "safesugar.net",
      "#下两行谷歌广告",
      "googleads.g.doubleclick.net",
      "adservice.google.com",
      "#【以下全部是geo预定义域名列表】",
      "#下一行包含所有私有域名",
      "geosite:private",
      "#下一行包含常见大陆站点域名和CNNIC管理的大陆域名，即geolocation-cn和tld-cn的合集",
      "geosite:cn",
      "#下一行包含所有Adobe旗下域名",
      "geosite:adobe",
      "#下一行包含所有Adobe正版激活域名",
      "geosite:adobe-activation",
      "#下一行包含所有微软旗下域名",
      "geosite:microsoft",
      "#下一行包含微软msn相关域名少数与上一行微软列表重复",
      "geosite:msn",
      "#下一行包含所有苹果旗下域名",
      "geosite:apple",
      "#下一行包含所有广告平台、提供商域名",
      "geosite:category-ads-all",
      "#下一行包含可直连访问谷歌网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:google-cn",
      "#下一行包含可直连访问苹果网址，需要替换为加强版GEO文件，如已手动更新为加强版GEO文件，删除此行前面的#号使其生效",
      "#geosite:apple-cn"
      ],
      "protocol": []
      },
      {
    "type": "field",
    "port": "0-65535",
    "outboundTag": "proxy"
    }
    ]

## 全局代理
所有上网连接全部走代理。


        [
          {
            "port": "",
            "outboundTag": "block",
            "ip": [],
            "domain": [
              "#阻止CrxMouse鼠标手势收集上网数据",
              "mousegesturesapi.com",
              "#下一行广告管理平台网址，在ProductivityTab（原iChrome）浏览器插件页面显示",
              "cf-se.com"
            ],
            "protocol": []
          },
          {
            "type": "field",
            "port": "0-65535",
            "outboundTag": "proxy"
          }
        ]

## 全局直连
所有上网连接全部直连。

        [
          {
            "port": "",
            "outboundTag": "block",
            "ip": [],
            "domain": [
              "#阻止CrxMouse鼠标手势收集上网数据",
              "mousegesturesapi.com",
              "#下一行广告管理平台网址，在ProductivityTab（原iChrome）浏览器插件页面显示",
              "cf-se.com"
            ],
            "protocol": []
          },
          {
            "port": "",
            "outboundTag": "proxy",
            "ip": [],
            "domain": [
              "#下一行ProductivityTab（原iChrome）浏览器插件",
              "ichro.me"
            ],
            "protocol": []
          },
          {
            "type": "field",
            "port": "0-65535",
            "outboundTag": "direct"
          }
        ]
## 全局阻断
阻断所有上网连接。

        [
          {
            "type": "field",
            "port": "0-65535",
            "outboundTag": "block",
            "ip": [],
            "domain": [],
            "protocol": []
          }
        ]

### 几点重要说明
- 路由规则中的中文说明，不需要删除，这都是以“#”开头的注释行。当然，也可以删掉，也可以自己添加。
- 自定义添加规则后，一定以英文逗号“,”结尾，不然会导致全部规则失效。
- 这些V2RayN高级路由功能策略代理规则，是个人使用并不断完善起来的，其中个别网址未必适合所有人，可以自己添加或删减。
- 高级路由功能中“预定义规则集列表”中的各行规则，不要随意改变排列顺序。因为，越在上面的规则，优先级别越大。调整顺序后，也会改变代理模式。
例如，在黑名单PAC代理模式规则集中，第二行是“proxy”代理规则，如果里面添加了域名baiyunju.cc，而第三行“direct”直连规则中，也添加了baiyunju.cc这个网址，那么，因为第二行比第三行更靠前，因此baiyunju.cc会按照第二行的规则连接网络，忽略第三行的设置。

## 六、快速添加路由设置规则的方法
首先，了解一些基本的定义和规则：
- Proxy (代理)、Direct (直连)、Block (阻止)的含义
- Block (阻止)： 拦截向外发送的连接请求，禁止连网。
- Direct (直连)： 直接访问外部网络，不走代理。
- Proxy (代理)： 允许通过代理连接上网。

- 查看V2Ray连接日志信息中，每条URL后面是[direct]（直连），还是[proxy]（代理）。
鼠标拖动选择这个网址URL，点击右键，选择“快速添加路由规则(Ctrl+V)”，或者按快捷键“Ctrl+V”，即可复制该URL的同时，自动打开V2RayN的“路由设置”界面，如下图：
然后，在“路由设置”界面，切换到“直连的Domain或IP”选项卡，选择好位置，再次按快捷键“Ctrl+V”，就将该网址粘贴到指定位置了。

## 七、黑名单电报设置的方法
只需要将Telegram的远程IP地址 91.108.56.156 添加到V2Ray路由代理规则内就可以了。

## 八、 检查更新系统代理
点击V2RayN界面-"检查更新"
