---
title: MacOS 使用 brew 安裝 nvm 管理 node.js
date: 2021-08-10 10:32:13
tags: nvm
categories: FrontEnd
---

> 有些專案由於年代久遠，所以沒有辦法使用現在的 LTS 的版本，所以透過 nvm 來切換 node 的版本，以利開發速度

## 安裝 nvm

首先你必需裝好你的 brew ，在用 brew 安裝 nvm

```shell
brew install nvm
```

這個時候你會被建立出 `.nvm` 和 `.zshrc` 的檔案，然後在你的 `.zshrc` 的檔案中加入下列的內容

```shell
export NVM_DIR="$HOME/.nvm"
[ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"
[ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"
```

`:wq` 存擋後退出，重新的去執行一段

```shell
source ~/.zshrc
```

然後確認一下 nvm 是否有安裝完成

```shell
nvm -v # 確認是否有版本
```

## 透過 nvm 來安裝 node

```shell
nvm ls-remote # 看有多少版本可以裝
```

選擇其中的一個版本來安裝

```shell
nvm install 12 # 安裝 v12 LTS 版本
nvm install 10 # 安裝 v10 LTS 版本

# 如果你要刪除的話
nvm unistall 10
```

安裝好了之後可以看一下你已安裝好的版本

```shell
nvm ls
```

在來就是你可以隨意的切換版本

```shell
nvm use 12 # 切到 node v12
```

> 常用到的 nvm 指令
>
> ```shell
> nvm ls
> nvm ls-remote
> nvm alias default [version] # 指令以後預設啟用的Node.js 版本
> nvm user [version] # 使用[version] 版本，但不更改預設啟用的版本
> ```

[參考資料](https://qizhanming.com/blog/2020/07/29/how-to-install-node-using-nvm-on-macos-with-brew)
