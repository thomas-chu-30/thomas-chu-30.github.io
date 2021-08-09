---
title: Mac 目錄結構
date: 2021-08-08 13:53:16
tags: mac
categories: 學會用你的 mac
---

## **Mac OS 系統目錄介紹**

max os 屬於類 unix 的系統，所以他會有一些 unix 系統的目錄風格。

網上對類 unix 系統的一些解釋

> 類 Unix 系統（英文：Unix-like）是指繼承 UNIX 的設計風格演變出來的系統（比如 GNU/Linux、FreeBSD、OpenBSD、SUN 公司的 Solaris、Minix、QNX 等），這些作業系統雖然有的是自由軟體，有的是商業軟體，但都相當程度地繼承了原始 UNIX 的特性，有許多相似處，並且都在一定程度上遵守 POSIX 規範，但是它們卻並不含有 UNIX 的原始碼。目前 UNIX 的原始碼為 SCO 公司所有，屬於商業軟體，UNIX 的商標權和 UNIX 標準認定屬於 OPENGROUP 所有。由於 UNIX 標準認定價格昂貴，所以目前唯一獲得 UNIX 標準認定的為蘋果的 MACOS 系統。

**以下目錄為類 unix 系統的通用目錄**

```bash
/bin
#bin是binary的簡寫，主要是一些系統必備的工具比如，cp,ls,mv,rm,sh等
#英文解釋：commands in this dir are all system installed user commands

/sbin
#sbin是管理員用於管理系統的一些必備命令，比如常用的，ifconfig,mount,reboot,shutdown等
#英文解釋：commands in this dir are all system installed super user commands

/usr
#目錄下面的基本都是系統自帶第三方和用戶安裝的第三方軟體的安裝目錄

/usr/bin
#用戶和管理員都需要用到的一些第三方軟體

/usr/sbin
#管理員可以用到的一些第三方的軟體

/usr/local/
#用戶自己安裝的一些第三方軟體所在位置

/usr/local/bin
#此目錄下一般都是用戶自己安裝的一些軟體的二進位文件入口，比如上一篇文章中提到的用homebrew安裝的nginx,他的執行文件軟連就在此目錄，例如：nginx@ -> ../Cellar/nginx/1.15.8/bin/nginx。可以看到他就是執行homebrew安裝的軟體位置。放在這裡的原因主要是在系統變量裡面 echo $PATH 已經配置/usr/local/bin 目錄，軟體軟連到此目錄後，命令行上直接輸入命令就能執行了。方便軟體的管理

/usr/local/etc
#一些第三方軟體的配置信息，比如之前說的nginx，就在此目錄：/usr/local/etc/nginx

/etc
# 用於存放系統配置文件的地方，如用戶密碼文件/etc/passwd，目錄指向的實際目錄是：/private/etc

/tmp
#臨時文件存放目錄，其權限為所有人任意讀寫。目錄指向的實際目錄是 /private/tmp

/var
#存放經常變化的文件，如日誌文件，目錄指向的實際目錄是 /private/var

```

**下面是 mac os 獨有的一些目錄**

```
/Applications
#基本一些gui應用程式都在此目錄

/Users
#用戶目錄，存放用戶的一些文檔，資料信息

/System
#只包含一個名為Library的目錄，這個子目錄中存放了系統的絕大部分組件，如各種framework，以及內核模塊，字體文件等等。

/Library
#系統的數據文件、幫助文件、文檔等等
```

原文網址：

[https://kknews.cc/code/8gg8zje.html](https://kknews.cc/code/8gg8zje.html)
