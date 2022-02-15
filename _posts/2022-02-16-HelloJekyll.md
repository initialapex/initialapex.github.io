---
title: Hello Jekyll
categories: Blog
tags: Jekyll Web Note
---

在工作上 Markdown 一直都是我筆記所使用的語法，甚至是我寫文件的方式；從開始想寫技術 Blog 後，找了很多支持 Markdown 語法的平台，像是 Medium, Blogger 還有點部落等等的平台，但是在線上編輯實在是不符合我的胃口，最終發現了 Jekyll 支持 GitHub Page 的方式，簡直太讚了，可以離線編輯，然後用 Git 的方式紀錄我的撰寫歷程，使用 Git Command Push 爽感，最後搭配 GitHub Auto Deploy，簡直是為了軟體工程師打造的環境啊～ 雖然我的 GitHub 似乎是個廢墟，但要開始寫技術筆記或許會越來越常使用吧

建置 Jekyll 至 GitHub Page 其實相當容易，簡略說的話，大概就是三個步驟，完成這三個步驟，就可以在設定的頁面上看到空空的部落格囉
- 建置環境
- 建立 JekyII 框架
- 建立自動部署檔案

## 建置環境

首先要先確認你的 Ruby 與 Gem 版本，說明可參考 Jekyll 的[官方說明](https://jekyllrb.com/docs/installation/#requirements)，個人是使用 Mac 這邊紀錄我安裝時所用的語法

安裝 Homebrew
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

安裝 Ruby
``` bash
brew install ruby
```

修改系統 Ruby 重新指向 `brew` 安裝的 Ruby，修改 `.zshrc` 檔案，在最後加上
``` bash
if [ -d "/opt/homebrew/opt/ruby/bin" ]; then
  export PATH=/opt/homebrew/opt/ruby/bin:$PATH
  export PATH=`gem environment gemdir`/bin:$PATH
fi
```

關閉所有的 Terminal 視窗再次重開後，確認 Ruby 的版本，如果版本顯示 `2.9` 以上就 OK 囉
``` bash
ruby -v
```

接著安裝 Jekyll 與 Bundler，電腦是**macOS 10.14**以上版本可參考下列語法安裝
``` bash
sudo gem install bundler
sudo gem install -n /usr/local/bin/ jekyll
```

這樣子前置的作業就差不多了，官方 macOS 安裝方式可以參考[這篇](https://jekyllrb.com/docs/installation/macos/)

## 建立 JekyII 框架

在建立專案上有很多種方式，有 Jekyll 官方的建立或是從別人 GitHub 上 Fork 出來，我個人是挑選了 [Chirpy](https://chirpy.cotes.page) 當作是我的主題，並利用他提供的[初始化](https://github.com/cotes2020/chirpy-starter/generate)方法

![Create from Starter](/assets/images/2022-02-14-Create-GitHub-Page.png)
輸入完你的網站名稱格式為 `{your-website-name}.github.io` 就可以建立一個空白的 JekyII 框架在你的 GitHub 上了

## 建立自動部署檔案

針對網站的內容設定的部分，則是修改 `_config.yml` 檔案內容，發布文章則是在 `_posts` 資料夾內建立起 `yyyy-mm-DD-title.md` 這樣格式的檔案，就可以讓 Jekyll 在 Build 的時候自然會吃到文章。修改後可以在自己的本機端做測試，利用 Bundler 安裝相關的插件，並建立網站
``` bash
bundle install 
```

在本機端讓網頁跑起來
``` bash
bundle exec jekyll s
```

跑完上述的 Script 之後，會在目錄上產生出 `Gemfile.lock`，為了要讓 GitHub Pages 能夠順利的自動部署，記得要將 Remote 端的 Build 環境給加進去，輸入下列指令
```bash
bundle lock --add-platform x86_64-linux
```

若網頁如預期的跑起來了，只要再利用 git 將修改的檔案 push 至 GitHub 上，經過自動部署後，就可以在所指定的網址看到成果囉

