---
title: Homebrew [NOTE]
date: 2021-08-19 17:17:16
tags: homebrew
categories: 學會用你的 mac
description: "mac 寫 code 的人必裝套件，紀錄此相關用法"
---

# Homebrew

```shell
# 安裝套件
brew search <formula>        # 尋找有無某套件
brew install <formula>         # 安裝套件
brew uninstall <formula>       # 移除套件

# update local packages
brew outdated                      # find out what is outdated
brew update                        # 更新 brew 本身和 formula
brew upgrade                       # 更新 brew 內的所有套件
brew upgrade <formula>             # 更新 brew 內的特定套件

# 移除舊版本（Homebrew 預設不會自動移除舊版本）
brew cleanup <formula>            # remove everything or specific formula of old versions
brew cleanup -n                   # see what would be cleaned up

# brew tap：適用於安裝不在 homebrew 的第三方套件（會增加 homebrew 的 formulae）
brew tap                      # list tapped repositories
brew tap <tap-name>           # add tap
brew untap <tap-name>         # remove a tap

# services
brew tap homebrew/services
brew services
brew services list                          # 看有哪些服務
brew services start [service_name]          # 開啟某個服務
```

## 安裝

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 透過 services 啟動資料庫等服務

```shell
brew install mysql
brew services start mysql
```
