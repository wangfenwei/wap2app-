

#翼达项目APP打包教程

---------
###一、编译打包流程

####  1.下载hbuliderx
下载地址：http://www.dcloud.io/hbuilderx.html

####2.新建项目
- 文件->新建项目->选择wap2app
- 填写项目名称（平台名称），填写首页地址（手机网页的首页地址，比如无界特训的：http://m.iydmall.com/index.php?i=81&do=mobile）

####3.修改配置文件（mainfest.json）
- 图标配置，选择一张1024的png运用图标，自动生成所有图标并替换
- 启动图配置，按尺寸对位一个个选择插入
- 模块权限配置，去掉Payment(支付)和push(消息推送)
- 源码视图添加urlscheme 

 ![avatar](http://ae01.alicdn.com/kf/HTB1DI6GMAvoK1RjSZFD760Y3pXae.png)

```
"distribute" : {
            "apple" : {
                "appid" : "", /*iOS应用标识，苹果开发网站申请的appid，如io.dcloud.HelloH5*/
                "mobileprovision" : "", /*iOS应用打包配置文件*/
                "password" : "", /*iOS应用打包个人证书导入密码*/
                "p12" : "", /*iOS应用打包个人证书，打包配置文件关联的个人证书*/
                "devices" : "universal", /*iOS应用支持的设备类型，可取值iphone/ipad/universal*/
                "frameworks" : [],
				"urltypes": [
					{
						"urlidentifier": "io.dcloud.wjtx",
						"urlschemes": ["81.iydmall.com"]
					}
				]
            },
            "google" : {
                "packagename" : "", /*Android应用包名，如io.dcloud.HelloH5*/
                "keystore" : "", /*Android应用打包使用的密钥库文件*/
                "password" : "", /*Android应用打包使用密钥库中证书的密码*/
                "aliasname" : "", /*Android应用打包使用密钥库中证书的别名*/
				"schemes": [
					"81.iydmall.com"
				],
                "permissions" : [
                    "<uses-feature android:name=\"android.hardware.camera\"/>",
```
####4.修改站点文件（sitemap.json）,直接拷贝下面的代码覆盖，需要修改matchUrls中的acid

![avatar](http://ae01.alicdn.com/kf/HTB1go2WMgHqK1RjSZFE763GMXXaj.png)
```
{
    "global": {
        "webviewParameter": {
            "titleNView": {
                "autoBackButton": true,
                "backgroundColor": "#f7f7f7",//导航栏背景色
                "titleColor": "#000000",//标题颜色
                "titleSize": "17px"
            },
            "statusbar": {
                //系统状态栏样式(前景色)
                "style": "dark",
				"background": "#ffffff"
            },
            "appendCss": "",
            "appendJs": ""
        },
        "easyConfig": {}
    },
    "pages": [
        {
            "webviewId": "__W2A__m.iydmall.com",//首页
            "matchUrls": [
                {
                    "href": "http://m.iydmall.com/index.php?i=81&j=&do=mobile"
                }
            ],
            "webviewParameter": {
                "titleNView": false,
                "statusbar": {
                    //状态条背景色，
                    //首页不使用原生导航条，颜色值建议和global->webviewParameter->titleNView->backgroundColor颜色值保持一致
                    //若首页启用了原生导航条，则建议将首页的statusbar配置为false，这样状态条可以和原生导航条背景色保持一致；
                    "background": "#f7f7f7"
                }
            }
        },
		{
		    "webviewId": "common",//首页
		    "matchUrls": [
		        {
		            "hostname": "m.iydmall.com"
		        }
		    ],
		    "webviewParameter": {
		        "titleNView": false
		    }
		}
    ]
}
```
####5.发行（APP云端打包）
- 安卓打包
单独勾选Android
选择使用DCloud证书
填写android包名，比如io.dcloud.wjtx，io.dcloud.（加平台名字拼音或自己起个名字）
去除广告联盟所有选项
打包，等待工具的左下角出先打包成功并返回apk下载链接
下载apk

![avatar](http://ae01.alicdn.com/kf/HTB1AZzTMbPpK1RjSZFF7615PpXam.png)


- iOS打包
单独勾选iOS
选择使用苹果证书
填写Apple AppId，比如io.dcloud.yd.wjtx，io.dcloud.yd.（加平台名字拼音或自己起个名字）
填写私钥密码，一般设置为123456
选择profile文件（需要后面申请生产描述文件，详细请阅读下面的申请iOS发布证书（.12文件）教程）
选择私钥证书（需要后面申请生产P12证书，详细请阅读下面的创建iOS发布描述文件（.mobileprovision文件）教程）
打包，等待工具的左下角出先打包成功并返回ipa下载链接
下载ipa

![avatar](http://ae01.alicdn.com/kf/HTB1fnjSMbPpK1RjSZFF7615PpXah.png)

---------
###二、安卓运用上架流程
####1.使用阿里运用分发开放平台
- 登录网址：http://open.uc.cn/login
- 使用淘宝账号登录
- 选择运用分发->安卓运用管理->创建软件
- 根据要求流程完成必填的选项，注意需要上传一张证明材料（上传资质证明，需要盖章）下载地址：http://img.ucdl.pp.uc.cn/upload_files/app_open_platform/docs/%E9%98%BF%E9%87%8C%E5%BA%94%E7%94%A8%E5%88%86%E5%8F%91%E5%BC%80%E5%8F%91%E8%80%85%E5%A3%B0%E6%98%8E%E6%96%87%E4%BB%B6.doc
- 填写材料无误，提交运用审核。

![avater](http://ae01.alicdn.com/kf/HTB18qfZMhTpK1RjSZR0762EwXXa5.png)

###三、iOS运用上架流程
####1.创建应用App ID
- 登录开发者中心https://developer.apple.com/account，进入证书页面，点击下图红圈处，进入设置。

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2017/05/1.1-1.png)

- 选择侧边栏App IDs –>点击右上角+号，添加一个新的App ID 
![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2017/05/1.2-1.png)
第一项Name，用来描述你的App ID，这个随便填，没有什么限制，（不允许中文）比如你的app叫无界特训，可以设置为拼音wujietexun
第二项Bundle ID (App ID ），APP的身份证号。填写App ID 的格式为：io.dcloud.yd.wjtx（要有两个点.）如app名字是无界特训可以编成io.dcloud.yd.wjtx，随便编，好记就行了。
- 下一步默认直接Continue。
- 下一步直接点击Register后点击Done完成App ID的创建。

####2.申请iOS发布证书（.12文件）
- 下载安装Appuploader工具
下载地址：http://www.appuploader.net/appuploader/appuploader_win_x86_64_jre.zip
- 打开Appuploader，用苹果开发者账号登录。

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2017/11/1.png)

- 选择证书选项

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2017/11/2.png)

- 点击右下角+ADD选择，下拉选择发布证书
证书名称：不要中文、随意设置
邮箱：随意
密码：123456
应用id：这里不用选
点击ok创建。
- 创建成功后，找到刚创建的发布证书（iOS Distribution这个类型的就是发布证书，如果之前创建过请看过期时间就知道哪个是新创建的了），点击p12 文件,下载保存.p12证书文件到电脑。（hbuliderx云打包用到）

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2018/08/8-1.png)

####3.创建iOS发布描述文件（.mobileprovision文件）
- 返回Appuploader首页，选择描述文件

![avater](http://www.applicationloader.net/blog/wp-content/uploads/2018/08/5-3.png)

- 点击+ ADD，选择发布版描述文件，
选择应用id：勾选上个步骤申请的发布证书p12（如果申请了多个发布证书，这里会显示多个，直接选中全部就行了）
这里不用选择设备。
输入名称（不用中文，随意，123之类的就行，注意不要跟之前申请过的名称一样），点击ok创建。
2.3、选择刚创建的发布版描述文件（iOS Distribution这个类型的就是发布描述文件，找刚创建的输入的名称），点击Download下载，保存到电脑

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2018/08/10-2.png)

####4.app store connect创建APP
- app store connect 登录网址：
https://appstoreconnect.apple.com/WebObjects/iTunesConnect.woa/ra/ng/app
- 进入点击左上角+号选择新建APP，选择平台iOS，
应用名称：APP的名称
语言：APP的语言，中文还是英文。
套装ID：（应用id、appid、包名，跟申请证书使用的要保持一致）
sku：不能写中文，自己用拼音随便编一个，好识别就行，如app叫无界特训，就输入io.dcloud.yd.wjtx。
用户访问权限：一般选完全访问权限
- 点击创建
- 完成后续的内容必填选项（注意此时构建版本是无法选择，需要后面的步骤的上传ipa包才能选择）

![avatar](http://ae01.alicdn.com/kf/HTB13M_Ge_Zmx1VjSZFG761x2XXaP.png)


####5.上传IPA包到App Store connect
- 打开Appuploader工具，选择上传单个ipa

![avatar](http://www.applicationloader.net/blog/wp-content/uploads/2018/08/3-4-1024x658.png)

- 选择上面  hbuilderx工具发行（APP云端打包）步骤下载得到ipa文件
- 等待出现下面的界面则代表上传ipa成功（可能需要10分钟）

![avater](http://www.applicationloader.net/blog/wp-content/uploads/2017/05/3-5.png)

####6.再次回到app store connect 设置APP各项信息提交审核
- 填写完整APP各项信息，上传不同尺寸的app屏幕快照
- 选择构建版本
- 提交审核
