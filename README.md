# MiAir-Hackintosh 

Hackintosh for my MiAir_i77500u

Thanks for the help of ourfor, his github address is
https://github.com/ourfor/Mibook-air

For now, Mi laptop is only sold in China, so this repo targets to help Chinese friends.

# Notice

MacOS EFI is [here](https://github.com/billhhh/MiAir-Hackintosh/releases)

# Hackintosh Step

## 手动建立ESP

DG软件在这一步骤用有很大作用，因为mac需要200M的EFI才能抹盘

我的自带EFI+MSR只有100M+16M=116M，所以要手动建立

（1）进DG将原始EFI分区备份（右键复制到桌面），并制作镜像（右键保存到镜像）

（2）从C盘中压缩一个400M的盘

（3）进DG，将这个400M的空白盘新建一个EFI system partition的盘，从镜像中恢复

这里如果出现写磁盘错误，重启可解决（这里卡了挺久）

## 做启动U盘

（1）用TransMac做U盘，注：我用的10.13的系统

（2）复制已经做好的EFI到U盘的ESP分区，有两种方法。一种是直接用explorer++；另一种是参照这个视频：https://www.bilibili.com/video/av19235761，将U盘ESP删除，新建一个FAT32格式分区，再把EFI复制过来

因为我用的10.13的系统（http://pan.baidu.com/s/1kVwxCPL），就用的相对比较旧一点的efi文件，这个repo里面的EFI_小米笔记本Air-i7-7500U-10.13.zip
用太新的efi，无限重启，后来得知kext文件夹中coredisplay需要去掉就可以用了，这个就是导致无限重启的原因
特别注意，driver64UEFI文件夹中的EmuVariableUefi64，这个用于驱动独显，但是现在版本驱动不了用不到

## 安装

压缩C盘空间空出一个40G的盘
值得一提的是，有很多教程建议这个时候将这个空白盘抹成apple的
我也是参照这个视频https://www.bilibili.com/video/av19235761，新建盘但是不分配盘符和格式化，也是可以的

另外还有一个问题：win的盘，可以读但是不能写，这个可以修改，但是windows系统分区不能写
其他ntfs的分区可以，百度或者Google macOS原生读写ntfs，不建议安装ntfs读写软件，这样对Windows系统分区不好

efi好了以后，安装就问题不大了，注意不要登陆就好，后面三码合一
安装后，进win，将Clover文件夹复制到硬盘
bootice添加 /ESP/EFI/CLOVER/CLOVERX64.efi 启动项，并移动到第一个

## 完善

～～三码合一参考：https://www.bilibili.com/video/av20912880～～
其实现在可以不用管三码问题了，直接拖入efi即可
另外直接装完以后可能唤醒有点问题，用10.13.3（https://pan.baidu.com/s/1bqmWMLp 密码: 7pu8），配合ourfor最新的efi（https://github.com/ourfor/Mibook-air/archive/5.0.zip）也可以解决

---------------------------20200303 更新---------------------

整理文件夹，分类摆放文件夹，Trackpad updated + 10.15 supported，现在触控板非常好用，可以三指拖动和三指查词等白果手势

Wireless Adapter driver: https://github.com/chris1111/Wireless-USB-Adapter-Clover

WiFi目前无解，国外大佬的IntelWifi项目进展迅速，目前已经能够在系统偏好设置-网络-Wi-Fi中扫描到WIFI信号了 相关项目地址：IntelWifi(https://github.com/rpeshkov/IntelWifi) 和 black80211(https://github.com/rpeshkov/black80211)

最新 efi 以 release 为准，如果是 Mi-Air-i77500u 可以直接拖入 esp 分区，目前已是黑苹果单系统

如果出现睡眠不醒的情况，请刷 tools/bios，此 bios 是0705版本的，可以参考教程 https://www.xiaomi.cn/post/105392

另外据悉，苹果公司有望在今明两年在 mac 上用上 ryzen，说不定以后有希望用更高性价比吃上黑苹果

贴一下 macos catalina 的下载地址：

（1）10.15 https://blog.daliansky.net/macOS-Catalina-10.15-19A583-Release-version-with-Clover-5093-original-image-Double-EFI-Version.html

百毒云下载链接: https://pan.baidu.com/s/1yAE6hUveviU6gKaEG0z_Yw 提取码: wqre

(2) 10.15.1 https://blog.daliansky.net/macOS-Catalina-10.15.1-19B88-Release-version-with-Clover-5098-original-image-Double-EFI-Version.html

百毒云下载链接: https://pan.baidu.com/s/1OG8Dm88bH66A38E0_ek0yg 提取码: 5tub

（3）10.15.2 https://blog.daliansky.net/macOS-Catalina-10.15.2-19C57-Release-version-with-Clover-5100-original-image-Double-EFI-Version.html

百毒云下载链接: https://pan.baidu.com/s/1LVbWZ-qLd8xQwQCsJct_bA 提取码: rk3d

（4）10.15.3 https://blog.daliansky.net/macOS-Catalina-10.15.3-19D76-Release-version-with-Clover-5103-original-image-Double-EFI-Version.html

百毒云下载链接: https://pan.baidu.com/s/1T7azCnptCdnw6qI41QghgA 提取码: kq67


---------------------------20180408 更新---------------------

### 解决无限重启问题

用ourfor v5 20180406的也可以了，删除Kext文件夹里面的coredisplay就可以用了，这个是修复显卡的驱动，可能和这个版本不兼容吧


因为model太新，三码合一用不了，不过也无大碍
清理Kext缓存软件：Kext Utility.app

### 开HiDpi

参考教程：https://ourfor.top/2018/01/01/%E5%BC%80%E5%90%AFhidpi/

配置文件：DisplayVendorID-9e5.zip

同时需要配合 RDM：https://github.com/avibrazil/RDM

RDM系统启动方法是
For more practical results, add RDM.app to your Login Items in System Preferences ➡ Users & Groups ➡ Login Items. This way RDM will run automatically on startup.

我的机器高清模式下，1280*720不错

### 耳机声音小

声音-平衡-最左 或者最右

### clover默认启动Windows

clover configuration打开config.plist，参考如下链接自定义clover
http://ourfor.top/2018/01/13/%E4%B8%AA%E6%80%A7%E5%8C%96clover%E5%90%AF%E5%8A%A8%E9%A1%B9/

目前的问题主要是：

（1）蓝牙不能用

（2）合盖休眠黑屏，只能强制关机。所以用黑果目前只能关机，用HibernationFixup.kext没什么鸟用，http://www.heimac.net/index.php/archives/488/

（3）电量不抗用，应该是cpu变频没弄好

（4）WiFi不能用，我买了comfast网卡，但是只支持2.4G单频，应该买双频，推荐EDUP双频600M迷你无线网卡
360网卡GitHub有，但是很久没维护了：https://github.com/tonyxiahua/360WIFI-MAC

（5）貌似有了plist，亮度还是不保留，不过这个问题不大

（6）显示器接口数据还没弄，不要通过HDMI接显示器，系统会崩溃的，


---------------------------20180409 更新---------------------

### parallels desktop装Ubuntu的时候内核崩溃

mac崩溃重启，开机的时候出现五国文字
开机在clover界面，按F1，再按f11，清除nvram，一般可以解决

另外小兵说的合盖唤醒不了不管用

### HDMI fix

之前说系统会崩溃，需要修改下接口数据，具体教程详见：
https://blog.daliansky.net/Display-interface-data-and-parameter-changes.html

https://blog.daliansky.net/Intel-core-display-platformID-finishing.html

把机型设成MacBook Pro14.2，应该clover里面打下补丁就行了，最好新建分区做时光机器备份
可以进mac，不过卡得要是，时常卡死，可以clover进recovery
按f几可以显示隐藏的recovery preboot分区
具体是f几，你可以按f1 help

---------------------------20180410 更新---------------------

半夜手残，想搞合盖休眠，dark=0，加了cms驱动，后来将苹果系统盘前面的116M分区删掉了，clover里面苹果的entry都没了，恢复clover也没用,怀疑是入口找不到了
apfs驱动在，U盘efi也不行
尝试time machine恢复，一直在搜索time machine界面，于是去分区助手看看，发现macos盘和time machine盘都未装载
准备重装10.13.3，80g做主盘，40g做tm盘
这说明，以后不是逼不得已，不要动分区

因为是最新10.13.3，可以用ourfor v5的efi（去掉一下emu独显驱动即可）：
https://github.com/ourfor/Mibook-air/releases


---------------------------20180414 更新---------------------

close lid问题解决了！！！不是网卡驱动问题，是DSDT跟BIOS有关

我的原BIOS版本日期是：Insyde Corp. XMAKB3M0P0907, 16/10/2017

现在需要刷成 XMAKB3M0P0705_MFG

刷了就可以用了！！！（刷的过程全程插电，不要动，等他自动重启）详见：http://bbs.xiaomi.cn/t-13100333
和 http://bbs.xiaomi.cn/t-13643021-2-o1#comment_top


唤醒有时会睡醒无声，不过很少见
可以安装 “睡眠唤醒 fixed” 文件夹里面的声卡驱动解决
另外记得清空缓存，用 Kext Utility.app

reset nvram一般不用，这和启动信息保存有关的


至此，黑苹果98%完美
还有网卡唤醒需要重新插上的问题，换一个网卡就好，EDUP EP-AC1620 11AC双频600M USB无线网卡：http://item.jd.com/3240026.html#comment


---------------------------20180415 更新---------------------

网卡唤醒，安装专用驱动解决

---------------------------20180716 更新---------------------

法1:打补丁是直接把 HDMI_fix/config.plist.fixed 替换就好了，但是这样的话就会启动项的名字就不一样了

法2:也可以把这段补丁代码直接粘贴到自己的 config.plist 文件里面

文本搜索 "外接HDMI显示器补丁" 可以找到增加段落，把那一部分的'<dict>…</dict>放到<key>KextsToPatch</key>的<array></array>'里面就行了

法3:或者你直接在这个软件里面加一个，把对应部分粘贴进去

建议清除下驱动缓存，然后重启

---------------------------20180801 更新---------------------

对于ourfor github里面2018年7月31日的，如果只想用新的触摸板驱动，其他不动，应该酱紫操作

```
首先备份你现在的EFI
- 删除ApplePS2SmartTouchPad
- 更新驱动VoodooI2C  VoodooI2CELAN VoodooI2CHID
- 更新DSDT，位于EFI/CLOVER/ACPI/patched/，更新DSDT.aml文件即可
重建缓存
```

另外，有个工作可以follow，GitHub有个小哥开发Wi-Fi模块，现在已经可以扫描到外部网络

https://github.com/rpeshkov/IntelWifi

https://www.tonymacx86.com/threads/intel-wifi-driver-effort.186344/page-23

---------------------------20180817七夕更新-----------------------

```
ourfor最新版的地址详见：https://github.com/ourfor/Mibook-air/blob/master/Changelog.md
最新版efi下载地址：链接: https://pan.baidu.com/s/16TsXGqDaI8W4mfP73TACqA 密码: 27hv
但是直接用可能有点问题，因为不一定是建立在esp分区
```

另外cpu驱动直接用黑果小兵的，他的也是7500U（github上面看看daliansky的dell的仓库），直接使用CPU friend那两个文件，相当于与原来一样

新触摸板驱动使用体验：
```
1、手势不错，但是进win，重启到mac还是不能用
2、但是键位的变化，键盘驱动在Apple2S…文件内部，感觉并不是太好用，alt键快捷键变化，所以换回原来的驱动（如果要修改键位，里面有个plugin文件，有个键盘驱动作为插件加载，那个键盘驱动里面设置键位）
3、换成ourfor的文件后，发现hidpi木有了，要每次开机都需要rdp启动，解决方法：hidpi要取消勾选plist里面的edid（详见ESP_version内部的TIM图片20180817134420图片）
```

---------------------------20180824更新-----------------------

亲测取消勾选plist里面的edid，hidpi好使

而且双屏的时候，如果自己的屏幕是hidpi，连上HDMI接口，本机不显示，反而外接显示屏显示；后来将本机hidpi去掉，再连接就可以了，而且连接之后可以将本机的hidpi放回来


# 参考

https://blog.csdn.net/Scythe666/article/details/79677730
http://www.miui.com/thread-7419826-1-1.html
http://www.miui.com/thread-7601066-1-1.html
http://www.miui.com/thread-7574042-1-1.html
http://www.miui.com/thread-11363672-1-1.html
https://www.bilibili.com/video/av20442523/?spm_id_from=333.338.recommend_report.2
https://www.bilibili.com/video/av19235761/?spm_id_from=333.338.recommend_report.3

