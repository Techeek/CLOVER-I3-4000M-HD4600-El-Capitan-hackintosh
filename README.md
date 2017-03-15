# CLOVER-I3-4000M-HD4600-El-Capitan-hackintosh
## 黑苹果CLOVER引导 I3-4000M HD4600安装OS X 10.11
* 电脑型号：神舟（HASEE）优雅 A500C
* CPU：I3-4000M
* GPU：HD4600
* 引导方式：CLOVER
* 系统版本：Mac OS X 10.11 El Capitan

> 我的笔记本是神舟的HASEE A500C CPU是I3-4000M 显卡是HD4600卡，安装这个本子可把人折腾坏了。先是用CLOVER安装，五国还没看到就重启了，最后GOOGLE扒贴解决，原来要更改Fake CPUID和InjectKexts（附链接[https://www.yayaus.com/2015/01/15/10-10-yosemite-i3-4000m.html][2]）按照教程改config下配置。
```conf
<key>FakeCPUID</key>
<string>0x0206F0</string>
<key>InjectKexts</key>
<string>Yes</string>
```
> 我去，果然正常启动了，折腾几十分钟后，发现显卡一直无法检测，打开显卡检测，检测到4600了，但是显存依然是4m 不爽，继续扒贴。然后我找到了这个（[https://www.tonymacx86.com/threads/fix-intel-hd4200-hd4400-hd4600-mobile-on-yosemite.145427/][3]）果然还是谷歌好，吐槽下度娘，搜了半天都没啥进展。按照教程，更改如下：

```conf
<key>Devices</key>
<dict>
<key>FakeID</key>
<dict>
   <key>IntelGFX</key>
   <string>0x04128086</string>
<key>Graphics</key>
<dict>
  <key>Inject</key>
  <dict>
   <key>Intel</key>
   <true/>
  </dict>
  <key>ig-platform-id</key>
  <string>0x0a260006</string>
```
> 没错，检测到了，除了开机LOGO花屏外，其他均正常，不用改DSDT，也不用打啥驱动，显示完美解决。
***
### 然后，给各位提个醒：
* 1、如果我的帖子无法解决，请参考这个（[http://bbs.pcbeta.com/viewthread-1486647-1-1.html][4]）我用他的方法没有解决，你们可以试试。
* 2、如果我俩的方法均无效。请重装系统后再重试我俩的方法，一般情况下重装就能解决。
* 3、无法正常升级10.12，升级花屏，想升级的朋友就不用尝试了，等待大神解决。


  [1]: https://github.com/Techeek/CLOVER-I3-4000M-HD4600-El-Capitan-hackintosh
  [2]: https://www.yayaus.com/2015/01/15/10-10-yosemite-i3-4000m.html
  [3]: https://www.tonymacx86.com/threads/fix-intel-hd4200-hd4400-hd4600-mobile-on-yosemite.145427/
  [4]: http://bbs.pcbeta.com/viewthread-1486647-1-1.html
