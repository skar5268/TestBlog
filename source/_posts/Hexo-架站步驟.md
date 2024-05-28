---
title: Hexo 架站步驟
date: 2024-04-28 11:35:52
tags: 教學
---

> [Hexo 起源](https://zespia.me/blog/2012/10/11/hexo-debut/) / [Hexo 官網](https://hexo.io/zh-tw/)
<br>

## 一、環境建置

### 1. 安裝 [Node.js](http://nodejs.org/)

### 2. 安裝 [Git](http://nodejs.org/)

### 3. 確認是否安裝成功
``` bash
node -v
npm -v
git --version 
```

### 4. 安裝 Hexo
``` bash
npm install -g hexo-cli
```

### 5. 建立平台
``` bash
hexo init 部落格資料夾名稱
```
<br>

## 二、部落格文章

### 1. 建立部落格文件
``` bash
hexo new '部落格文章名稱'
``` 

### 2. 使用 [**Markdown 語法**](https://markdown.tw/) 撰寫文章

### 3. title 為文章標題
<br>

## 三、其餘指令說明

### 1. 於本機打開部落格預覽
``` bash
hexo server
``` 

### 2. 部署至網頁的資料夾
``` bash
hexo generate
```

### 3. 清除快取
``` bash
hexo clean
```

### 4. 將部落格部屬到 Github Pages
``` bash
hexo deploy
```

### 5. 新增部落格頁面
``` bash
hexo new page 頁面名稱
```
輸入指令後，將於 source 資料夾內新增**頁面名稱**的資料夾

## 四、部落格相關設定

### 1. 部落格基本資料
於 `themes > config.yml` 修改，以本部落格為例
``` bash
title: 阿若的 Hexo 部落格
subtitle: Hexo 部落格
description: 還不知道要放什麼東西
keywords:
author: 阿若
language: zh-TW
timezone: ''
```

### 2. 部落格客製化
#### - 安裝客製化樣板
```bash
git clone --depth 1 https://github.com/hexojs/hexo-theme-landscape themes/landscape
```
#### - themes 資料夾內將新增 landscape 資料夾
#### - 在 `landscape > source > config.yml` 可以修改 menu 等資料 


## 五、部屬到 GitHub 上
### 1. 將 VS code 綁定 GitHub 帳戶
### 2. 在 GitHub 上 create new repository
### 3. 在 GitHub Pages 上部署 Hexo
#### - `npm install hexo-deployer-git --save`
#### - 在資料夾最上層的 `config.yml` 檔案中，滑到最下面的 deploy 區塊（第 103 行），將下面程式碼貼上去
```bash
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
#### - 
```
#### - 於同樣的 `config.yml` 檔案中找到 URL（第 16 行），修改網址為自己的
[教學連結](https://hexo.io/zh-tw/docs/github-pages#%E4%B8%80%E9%8D%B5%E9%83%A8%E5%B1%AC)
### 4. 清除快取 & 將部落格部屬到 Github Pages
```bash
hexo clean && hexo deploy
```
### 5. 確認 GitHub pages 是否成功顯示

### 6. 套用其他模板
安裝模板後，於資料夾最上層的 `config.yml` 檔案中，第 99 行 theme 改成安裝的模板
