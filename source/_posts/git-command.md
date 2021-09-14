---
title: Git 時光之術
date: 2021-08-14 00:23:21
tags: git
---

> Git 可以說是比寫 code 還要重要的東西，現在的專案基本上都要共同協作，所以如何避免衝突，不在開發的時候發生災難，可以說是非常的重要，寫 code 寫不好可以問人，但 Git 不行的話可能連工作都沒有辦法一起 co-work 。
>
> 另外如果對 `vim` 還沒有很熟的話建議去多了解一下 `vim` 的編輯、儲存、查尋方式，對你在使用 git 上會更加的得心應手。

<!--more-->

# Git 常用 commend line

## git 起手式

在專案位置下初使化 git ，表示可開始用 git 來管理你的專案，此時專案中會出現一個隱藏資料夾 `.git` ，然而你在開發的過程中也一定會有你不想要推到 remote 的東西，這個時候你可以建立一個 `.gitignore` 的檔案，在裡面編寫你不想要上傳的文件 or 資料夾

```shell
git init
# .gitignore 檔案
node_modules # 資料夾不推上 git
/dist
.env # 檔案不推上 git
```

在來你需要對專案說，你是誰，所以把你的 email 和名稱和 git 說，因此在 git.config 裡面建立資訊

```shell
git config --list # 查看你目前的 config 清單
git config --global user.name [YOUR_NAME] # 建立名稱
git config --global user.email [YOUT_EMAIL] # 建立 email
```

## clone 專案

開發其它的專案，透過 clone 的方式，把 .git 的檔案一起抓下來

```shell
git clone [YOUR_PROJECT]
```

## 加入 remote

```shell
git remote -h # 查詢remote相關指令
git remote rename `<old>` `<new>` # 將遠端數據庫的名稱從 <old> 改為 <new>
git remote set-url `<name>` `<newurl>` # 在 <newurl> 內指定遠端數據庫的新地址
git remote add origin [YOUR_PROJECT]
```

## 切換遠端分支

首先你應該不會知道專案中所有的 br 叫什麼名稱，所以可透過

```shell
git branch -a # 查看所有 local 遠端 br
```

在確認完之後，在回到專案的位置上，進行切換分支

```shell
git checkout -b [BRANCH_NAME] [origin/BRANCH_NAME]
```

## 加入暫存區

把資料加入暫存區

```shell
git add . # add all file stage
git add -p # after everyone check, add file to stage
```

取消加入暫存區

```shell
git checkout
```

## 加入本地儲存區

把資料加入本地儲存區，方法其實有很多種，但主要就是要把你的資料寫到 git 裡面，如果你所要寫的東很多的話，建議你可以用 ` vim` 的方式去作編輯歐

```shell
git commit # 會直接進到 vim IDE 中
git commit -m 'msg content'
```

退回本地儲存區

```shell
git log # get commit id
git reset --hard `<id>^` # 本地數據庫不見
git reset --soft `<id>^` # 本地數據庫還在
```

> commit 訊息邏輯
>
> - 以大寫開頭
> - 以<動詞> + <受詞> + <內容> 的文法撰寫
> - 內容不宜過長
> - 內容需要據有代表性

## stash

會使用它最常有的情境是，你開發到一半，但是 BOSS 請你趕快的去處理另一件是，這個時候你也還沒有到可下 commit 的時候，這個時候，可用 stash 把你開發的 code 先到一個地方，之後只要回來，在把東西 stash 回來便可繼續開發。

> 在 stash 之前建議先把所有的 code 放到暫區，因有時候我們是新建檔，直接 stash 的話新檔就會被遺留在，原本的 br 上面
>
> ```shell
> git add .
> ```
>
> 為了確保我們所寫的東西不要被分別放在不同的 stash list 裡面

暫時存現狀

```shell
git stash save 'msg ...'
```

顯示暫存清單

```shell
git stash list
```

回復暫清單，通當你會去看一下你的清單有什麼，然後確定是第幾個之後用 `stash@{0}` 的方式來還原你想的的暫存。

> 這裡的 0 是表示，你最一次 stash 起來的東西，1 的話就是倒數第二次的東西，依此類推

```shell
git stash pop shash@{0} # 拿回最後一次 stash 的 code
git stash pop `<shash ID>` # delete stash data
git stash apply `<shash ID>`
```

刪除暫檔

```shell
git stash drop `<shash ID>`
git stash clear # clear all
```

# 合併分之

通常在有規模的專案下面開發，比較不會用到 merge ，因為主要都是透過 lib 去發 merge request ，而不是自己在本地，就把 code merged 到其它的分支。

## merge

```shell
git merge [BRANCH_NAME]
```

> 但是我們在拉分支的時候，其實就是常常在用 merge 的指令，只是被合併在一起了。

## rebase

```shell
git rebase [BRANCH_NAME]
```

> 這兩個都是把 br 作合並的效果，但是 rebase 是直接把原本的分支合回到另一個 br 的分支上，變成一個，也就是說，有些 commit 你可能會沒有辦法在 tree 上面直接的看到，因為被合到另一個 tree 上面了

# 刪除 branch

Coming soon ...

# 遠端數據庫

## fetch

主要只執行拉 code 的動作，但它不會把 code 和你現在的 br 進行合併，所以執行完後你是會在 `HEAD` 上面的

```shell
git fetch # 把你在遠端的 br 拉下來
```

## pull

那 pull 的這個動作，就是我們把 fetch + merge 的動作一起作完，把 code 拉下來，然後 merge 到你現在的 br 中

```shell
git pull # git fetch + git merge
git pull --rebase # 當然你也可選擇 rebase
```

## push

把你所 commit 好的的檔案往上傳到 remote 端，但是需先確認是否已設定好 origin 的 remote 位置

```shell
git push origin [BRANCH_NAME]
```

# tag

若要添加標示標籤，可以在 tag 命令加上 -a 參數執行，執行後會啟動編輯器，請輸入要給予的註解。也可以用 -am 參數來直接添加註解。

```shell
git tag -a [TAG_NAME]
```

在 HEAD 指向的提交裡增加名為 `[TAG_NAME]` 的標籤，請執行以下的命令。

```shell
git tag -am 'msg...' [TAG_NAME]
git tag -n #  可以顯示出標籤和註解
```

# Git Bisect

> 希望你一輩子都不要用到這個東西。

```shell
git bisect start [BAD_COMMIT] [GOOD_COMMIT]
# 開始後將自動 checkout 到要檢查的 commit
# 請執行以下指令標記正常 or 錯誤
```

[參考文章](https://www.gss.com.tw/blog/%E4%BD%BF%E7%94%A8-git-bisect-%E5%BF%AB%E9%80%9F%E6%89%BE%E5%88%B0%E7%AC%AC%E4%B8%80%E5%80%8B%E6%9C%89%E5%95%8F%E9%A1%8C%E7%9A%84-commit)

# fork 專案

在 `github` 選擇 fork ，需在把你的 remote 專案名稱修正，因為通常 origin 指的是自己的開發 remote。然後在把 fork 的 repositories 設定到你的 origin 裡面。

確認 remote 的名稱 ⇒ 修正名稱 ⇒ 加入新的 fork repositories ⇒ 確認 remote 的名稱

# Git alais

Coming soon ...

# 檢查 git

下列這些指令是在你開發到一半，想要回去查東西時很用的指令

```shell
git status # 看一下還有多少東西沒有進暫存區
git log # 確認這個 br commit 的狀況
git remote -v # 確認一下遠端
git stash list # stash 的清單
git remote -h # 可以檢看一下指令
```

# 參考文章

[搬移檔案](https://zlargon.gitbooks.io/git-tutorial/content/file/move.html)

[git commit message 的格式](https://www.notion.so/git-commit-message-a18a8a5cc0cb4cc48c4c49c82da4cabe)

[git commit 這樣子寫更好](https://wadehuanglearning.blogspot.com/2019/05/commit-commit-commit-why-what-commit.html)
