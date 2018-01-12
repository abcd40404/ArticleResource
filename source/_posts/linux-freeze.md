---
title: 解決 Linux 卡屏(Freeze)
date: 2018-01-12 11:41:53
tags:
categories: [學習札記, Linux]
---
昨天開機時
畫面一直停在
```
dev/sda5: recovering journal
/dev/sda5: clean 221608/30269440 files, 4431756/121048320 blocks
[  OK  ] Starting Anonymizing overlay network for TCP.
[  OK  ] Created slice User Slice or gdm.
         Starting User Manager for UID 121...
[  OK  ] Started Session c1 of user gdm.
[  OK  ] Started User Manager for UID 121.
         Stopping User Manager for UID 121...
```
查了一下又是圖形介面的問題, 安裝好新版 Nvidia driver 之後又可以運行了
所以寫了這篇, 寫我在 GDM 遇到的問題
我的顯示卡是： Nvidia Geforce GTX 660

約莫在兩年前, 想從 ubuntu 跳到 fedora 玩玩
裝好之後, 準備開始探索
用了一陣子之後, 我的滑鼠不能動了
嘗試一段時間, 發現原來是我的畫面整個卡住了！！
當時試著去解決他, 花了一整個禮拜
還是解決不了, 適逢期中考, 只好放棄
在 2017/10 我想要在桌電上使用 linux 阿！！
趁著大四比較閒, 又開始著手解決這個問題
很幸運的, 這次只花 2 天就解決了（我也不知道為什麼？

第一次遇到這個問題, 心想該不會是我的硬體和 fedora 不合吧
於是換回 ubuntu, 用了一陣子之後, 居然也會卡住！？
我裝 fedora 之前還好好的阿？？
於是我懷疑到 chrome 上, 因為卡住的時機點都是在我瀏覽網頁時
所以我就讓電腦什麼都沒開, 閒置在那邊
一段時間回來之後, 居然也卡住了...

後來又試了不同方法, 像是用別的電腦連線進來
用 htop 觀察 CPU 和 記憶體有沒有異常
完全沒有異常, 連 kernel 也是正常運作
所以可以確定, 是我的圖形介面死去了

於是我到 /var/log/syslog 查看
有幾行紅字(因為太久了, 我的 log 已經被洗掉, 所以拿別人的訊息)
```
kernel: nouveau E[  PGRAPH][0000:01:00.0] TRAP ch 8 [0x003f61d000 kwin_x11[697]]
kernel: nouveau E[  PGRAPH][0000:01:00.0] GPC2/TPC0/MP trap: MULTIPLE_WARP_ERRORS
kernel: nouveau E[   PFIFO][0000:01:00.0] read fault at 0x867e84f000 [PDE] from GR/GPC2/RAST on channel 0x003f61d000 [kwin_x11[697]]
kernel: nouveau E[   PFIFO][0000:01:00.0] PGRAPH engine fault on channel 8, recovering...
kernel: nouveau E[  PGRAPH][0000:01:00.0] TRAP ch 8 [0x003f61d000 kwin_x11[697]]
kernel: nouveau E[  PGRAPH][0000:01:00.0] GPC2/TPC0/MP trap:
kernel: nouveau E[  PGRAPH][0000:01:00.0] TRAP ch 8 [0x003f61d000 kwin_x11[697]]
kernel: nouveau E[  PGRAPH][0000:01:00.0] ROP0 0xbadf1200 0xbadf1200
kernel: nouveau E[  PGRAPH][0000:01:00.0] ROP1 0xbadf1200 0xbadf1200
kernel: nouveau E[  PGRAPH][0000:01:00.0] TRAP UNHANDLED 0xb8df1200
kernel: nouveau E[    PBUS][0000:01:00.0] MMIO read of 0x00000000 FAULT at 0x40010
```
上網查了一下 nouveau 是開源的 Nvidia driver, 很顯然的他出了問題
所以我決定要把他換成 Nvidia 提供的 driver
首先第一步就是要將 nouveau 給關掉
有蠻多人提供方法, 但有些都不可行, 所以我加到最後也不知道哪幾行是有作用的
總之就放上來提供參考：
到 etc/modprobe.d
```
sudo vim blacklist-nouveau.conf

在文件裡添加
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
接著到 tty1 ~ 7 都可以
按 Ctrl + Alt + F1 到 tty1, 我們要關閉圖形介面
```
sudo init 3
sudo rm /tmp/.X*
// 上面這兩行我忘記我當初有沒有打了

sudo service gdm stop
// 註： 我是用 gnome, 所以是 gdm 不是 lightdm

sudo sh NVIDIA-Linux-x86_64-384.111.run

sudo service lightdm start
//安裝完畢, 打開圖形介面
```

參考資料：
1. https://l.facebook.com/l.php?u=https%3A%2F%2Fask.fedoraproject.org%2Fen%2Fquestion%2F104629%2Ffedora-25-nouveau-crashing-upon-loading-gnome-shell%2F&h=ATMq1Af2QMA4q0aNjph_n8nB03GsXaMYgty7eALS1QHF-fRZlOC9XDgkVD9ImUopn5YsjWFtn8PNx73nX_YdNBAr9mgCwJM6JNV4C5kXqm9moiUq6iJf73wp_4HisnR9V-Qp1A
2. https://l.facebook.com/l.php?u=https%3A%2F%2Fbugs.freedesktop.org%2Fshow_bug.cgi%3Fid%3D89912&h=ATMq1Af2QMA4q0aNjph_n8nB03GsXaMYgty7eALS1QHF-fRZlOC9XDgkVD9ImUopn5YsjWFtn8PNx73nX_YdNBAr9mgCwJM6JNV4C5kXqm9moiUq6iJf73wp_4HisnR9V-Qp1A
3. http://www.itread01.com/content/1495718475.html
4. https://zh.wikipedia.org/wiki/LightDM
5. http://blog.sciencenet.cn/blog-655584-877622.html
6. https://www.openfoundry.org/tw/foss-programs/9265-xserver

