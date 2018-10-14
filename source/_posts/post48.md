---
title: NVDA无法下载升级的解决方案新增：注册演示
date: 2014-06-14 14:08
tags:
more: 详细阅读
---
在很多情况下，当我们尝试下载或者升级NVDA软件时会发生失败的情况，根据我的发现，可以使用DNSCrypt 和Goagent解决这个问题。下面是详细教程，希望能帮助到大家升级NVDA。
## 一、使用DNSCrypt规避DNS污染
[下载地址](http://shared.opendns.com/dnscrypt/packages/windows-client/DNSCryptWin-v0.0.6.exe)
请注意：卸载本软件如果方法不当，可能会清空DNS设置，请初学者慎用！
DNSCrypt-proxy 可当作是一个 DNS 代理服务器，用于提供 DNS 客户端和服务器之间的安全通讯。
DNSCrypt是一个确保客户与DNS服务器之间传输安全的工具，基于DNSCurve修改而来。
由于Domain Name System(DNS)设计上的缺陷，用户在浏览器里输入很多海外网址以后，如果遭遇MITM（Man in the Middle,中间人攻击）或者DNS污染，浏览器就可能接收到错误的IP而导致安全问题。为了解决这个问题，IETF在十几年前便开始制定DNS的安全 扩展（DNSSEC），主要是利用公开密钥加密技术，通过对DNS数据进行数字签名，DNSSEC能够验证DNS数据来源和验证在传输过程中DNS是否被 篡改。
但是DNSSEC不保证DNS数据的机密性，DNS数据本身并没有被加密，加之DNS的阶层式模式，这便 为一些机构提供监视，控制网络的手段，典型的例子就是不能访问一些海外的网站。DNSSEC也不提供免于DOS(Deny of Service，拒绝服务)攻击的办法，由于数字签名和签名验证需要额外的数据运算，DNSSEC反而更容易受到DOS攻击。DNSCurve相对于 DNSSEC的好处是，DNSCurve使用了更有效率的椭圆曲线加密算法而减少了运算量，可以对每条DNS查询都单独加密，从而更加安全。
DNSCrypt协议是非常类似DNSCurve的，作为一个DNS代理运行，侧重于客户端和第一级DNS服务器之间的通信安全，能够缓存DNS解析。DNSCrypt的上游DNS服务器是著名的OpenDNS服务，简单而言DNSCrypt就是加密了本机到OpenDNS服务器之间的DNS查询通信过程（使用椭圆曲线加密算法），所以可以不受GreatFireWall的DNS污染干扰。
安 装方法是首先下载对应平台的dnscrypt client然后运行，接着修改本地或者router的dns server为127.0.0.1. 然后你的所有dns请求都会加密进行从而绕过GreatFireWall的dns污染顺利解析到正确IP，以下是Win7系统设置的图示： （DNSCrypt可以在Windows/Linux/BSD/OSX/iOS系统上运行）
[以上介绍内容来自](http://hi.baidu.com/bgp90/blog/item/e9d632e5489ce2ce2e2e2118.html)
## 二、使用Goagent升级
[goagent下载页](http://www.sd173.com/html/1802.html)(后点击高速下载转到网盘下载页面。令付goagent的<a href="http://grmrw.5d4d.net/NVDACN/audio experiences/goagent注册演示（试讲）.mp3">音频演示</a>
## 申请Google App Engine并创建appid
注意，如果本页面无法访问，可以尝试使用http://www.q8daili.com/，使用网页代理进行访问，如果失败可多在“server”组合框更换服务器进行尝试。
1. 申请注册一个Google App Engine账号[打开地址注册](https://appengine.google.com)。没有Gmail账号先注册一个， 用你的Gmail账号登录。
2. 登录之后，自动转向Application注册页面，如下图：
3. 接下来的页面，输入你的手机号码，需要注意的是，手机号码前面要+86（中国区号） 格式如：+86 13888888888。
• 然后等待收取手机短信，收到短信后（一串数字号码）填入下图表单，点send提交.（有的手机收不到信息，解决办法：详细教程 到https://appengine.google.com/waitlist/sms_issues 提交该情况，一个工作日就能收到谷歌提示Google App Engine成功开通）。
4. 提交完成之后，GAE账号即被激活，然后就可以创建新的应用程序了。转入“My Applications”页面，点击“Create an Application”新建应用
• 一个Gmail账户最多可以创建十个GAE应用，每个应用每天1G免费流量。这里我们只创建一个应用就可以了。进入下一步，填写新应用的必要信息，如下图。在图中第一处添加一个应用名称，如abc555,验证一下是否可用，如果显示“Yes”那么abc555就是你的Appid（记住这个id），而abc555.appspot.com就是你的应用服务器地址了。第二个空可随便填，点击Create Application按钮提交
• 提交之后，就能看到下图这个页面，就说明你已经成功创建了一个新的应用,你也可以点击应用名称，进入控制面板进行管理。   
• 如果你要建立多个appid，只需要从步骤4开始再重复操作多次就行了。
## 下载goagent并上传至Google App Engine
1. 下载goagent并解压，[下载goagent](https://code.google.com/p/goagent/)
2. 编辑local\proxy.ini，把其中appid = goagent中的goagent 改成你之前申请的应用的appid (用windows的记事本也可以） 
• 如果要使用多个appid，appid之间用|隔开，如：appid1|appid2|appid3，每个appid必须确认上传成功才能使用 
[gae]
appid = appid1|appid2|appid3
3. 运行goagent.exe 
4. 上传 
• Windows用户：双击server文件夹下的upload.bat，输入你上步创建的appid（同时上传多appid在appid之间用 | 隔开,一次只能上传同一个谷歌帐户下的appid）填完按回车。根据提示填你的谷歌帐户邮箱地址，填完按回车。根据提示填你的谷歌帐户密码(注意：如果开启了两步验证，密码应为16位的应用程序专用密码而非谷歌帐户密码，否则会出现AttributeError: can't set attribute错误），填完按回车。如果要上传多个谷歌帐户下的appid，先上传一个账号的，传完一个账号后删除uploader.bat同目录下的.appcfg_cookies文件再传另一个 
• Linux/Mac OSX用户上传方法：在server目录下执行：python uploader.zip      <<更详细Linux平台使用方法>>
• 如遇到getaddrinfo failed，error10054，Error 10061 目标计算机积极拒绝等错误而不能上传，可以先运行goagent.exe(要先修改appid)再运行uploader.bat 
• 要使用IPv6上传或者上传遇到11004错误可以按照此贴进行修改和Issue 9288
• 上传成功就会看图下图界面
## 运行客户端
1. Windows用户运行local文件夹中的goagent.exe，   Linux/Mac OSX用户运行 proxy.py 
• 设置浏览器或其他需要代理的程序代理地址为127.0.0.1:8087 
• 注意：使用过程中要一直运行goagent.exe/proxy.py 
• 代理地址127.0.0.1:8087；如需使用PAC，设置pac地址为http://127.0.0.1:8086/proxy.pac；也可以配合SwitchySharp/AutoProxy等浏览器扩展（SwitchySharp用户可从local文件夹中的SwitchyOptions.bak文件导入配置）pac是什么？
2. 导入证书 
• IE/Chrome：使用管理员身份运行goagent.exe会自动向系统导入IE/Chrome的证书，你也可以双击local文件夹中的CA.crt安装证书（需要安装到“受信任的根证书颁发机构”）； 
• 下一步 -> 完成 -> 确定 
• Firefox：需要单独导入证书，打开FireFox?->选项->高级->加密->查看证书->证书机构(必须是这项)->导入证书, 选择local\ca.crt, 勾选所有项，导入； 
• opera：导入证书方法：首选项→高级→安全性→管理证书→证书颁发机构(必须是这项)->导入->选择local\ca.crt文件->依次确认； 
• 注意：请勿重复安装证书 
﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎ 
# 附：浏览器设置方法
1. 
使用GoAgent自带代理设置功能
• 该功能可以为IE/IE内核浏览器和未安装代理类扩展的chrome、opera等默认使用IE代理的浏览器和软件设置代理，但不能给FireFox设置代理 
1. 右击GoAgent托盘图标，在“设置IE代理”菜单中选择要使用的模式。 
1. 禁用代理    什么也不做，需要用户自己手动为软件设置代理 
2. http://127.0.0.1:8086/proxy.pac   使用自带的PAC自动判断是否使用代理 
3. http://127.0.0.1:8087    全部使用GoAgent代理 
2. 
谷歌chrome配合Proxy  Switchy Sharp扩展
1. 安装扩展 
• 地址栏输入chrome://extensions/后按回车，打开扩展管理页，将local文件夹中的SwitchySharp-0.9-beta-r48.crx拖拽到该页面之后点击确定即可安装，扩展也可以从chrome应用商店获得https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm
2. 导入设置 
• 点击 Proxy  SwitchySharp图标》选项》倒入/导出》
• 浏览到SwitchyOptions.bak，点击确定导入设置 
• 更新自动切换规则（如果遇到无法更新规则列表，可以先运行goagent，并把浏览器代理设置为GoAgent模式再更新规则，不更新规则只会影响自动切换模式，不会影响其他模式的使用，若确实无法更新也可不更新，直接使用PAC模式即可） 
• 在扩展设置页点击“切换规则”，点击“立即更新列表”，最后点击“保存”。
• 单击地址栏右侧Proxy  SwitchySharp图标即可进行模式选择 
1. GoAgent模式  除匹配proxy.ini中sites的直连外，其他全部通过GAE 
2. GoAgent PAAS模式   全部通过PAAS 
3. GoAgent PAC模式   根据GoAgent自带的PAC文件自动判断是否经过代理 
4. 自动切换模式 根据切换规则自动选择是否进行代理，并根据所设情景模式自动选择使用何种代理 
• 遇到规则中没有的，可以使用扩展的“新建规则”按钮自行添加，选情景模式为“GoAgent”，使用此模式可以方便的定制自己的代理切换规则 
• 这个扩展偶尔会出BUG，出现设置无误但浏览器提示错误130无法连接到代理服务器，可以将自己的设置导出之后卸载重装 
• 如果遇到无法更新规则列表，可以先运行goagent，并把浏览器代理设置为GoAgent模式再更新规则，不更新规则只会影响自动切换模式，不会影响其他模式的使用，若确实无法更新也可不更新，直接把扩展设置为GoAgent PAC模式即可 
3. 
Firefox配合Foxy Proxy扩展
1. 安装扩展https://addons.mozilla.org/zh-cn/firefox/addon/foxyproxy-standard/
2. 设置 
• 右击foxyporxy图标即可选择代理模式 
3. 添加代理规则订阅（可选） 
• 这里以添加gfwlist为例，你也可以自行添加其他规则订阅 
• 更多设置请自行探究 
4. 
Firefox配合Auto Proxy扩展(新版Firefox请将此扩展升级至最新版)
1. 安装扩展https://addons.mozilla.org/zh-cn/firefox/addon/autoproxy/
2. 设置 
1. 添加代理服务器   注意:新版autoproxy已内置GoAgent配置，可直接进行下一步
2. 添加规则订阅 
3. 选择自己需要的模式 
1. 自动模式   根据规则自行选择是否使用代理 
2. 全局模式   全部使用代理 
3. 禁用代理   全部不使用代理 
5. 
opera浏览器设置
同IE一样样有两种方式可选，不过不会影响系统其他程序的联网  
1. 设置代理为127.0.0.1:8087，全部使用goagent代理 
• 不使用时应恢复为无代理状态 
2. 使用PAC自动代理 
• 如果你喜欢折腾的藕粉，也可以按照这篇文章（比较复杂）自己做一个方便切换的按钮，当然还有精简版的
6. 
IE浏览器设置（不建议）
• IE有两种方式，分别为全部使用goagent代理和是pac自动代理，很多软件都使用IE代理设置，可能影响部分软件的联网，「不建议设置IE代理」 
• 工具》Internet选项》连接，局域网用户单击"局域网设置"。宽带用户选中自己正在使用的宽带连接之后单击"设置"，不要选“局域网设置”
• 局域网用户设置方法
1. 设置代理为127.0.0.1:8087，全部使用goagent代理（不建议） 
2. 使用PAC自动代理 
• 宽带用户设置方法
1. 选中自己正在使用的宽带连接之后单击"设置" 
2. 设置代理为127.0.0.1:8087，全部使用goagent代理（不建议） 
• 不使用时要将IE恢复无代理状态 
﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎﹎ 
goagent适用环境
• 适用：浏览器，支持http代理的下载软件等 
• 不适用：游戏客户端等需要稳定网络的程序，QQ，tor（验证证书）。待添加。。。 
关于软件更新
• 更新历史中带有[是]则需要重新上传，否则不用重新上传。注意：是否需要重新上传是相对于前一版的，若你之前版本与当前版本之间某一版或多版带有[是]仍然需要重新上传。 
• appid并不绑定任何客户端，如果本次更新无需重新上传，只需修改proxy.ini中的appid即可使用。同样，你也可以把appid共享给朋友，或者在自己其他机器上使用，一个appid可以多人多机器同时使用，在无需更新服务端的情况下，只需成功上传一次即可。在没有设定密码的情况下，只需要知道appid就可以使用你该appid的流量，为防止被盗用可以加上密码。 
• goagent每一版下载的都是全部文件，你可以选择覆盖原文件或者将新版放另一个文件夹，旧版你可以选择留存或者删除，修改新版proxy.ini中相关设置即可运行。如果旧版添加了开机启动，需要将旧开机启动删除。如果旧版已经在运行，需先将旧版关闭。 
• 如果之前版本没有ssl错误，使用新版出现ssl错误可以把原来的ca.cer、ca.key和certs文件夹内的文件覆盖当前的这些文件。或者将ca.cer、ca.key和certs文件夹内的文件全部删除，同时删除浏览器中所有goagent ca的证书，再重启goagent，会生成新证书，重启浏览器再导入新证书即可。浏览器证书中只能有一个goagent ca的证书。 ﹎