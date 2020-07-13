---
title: NPM小技巧
date: 2020-07-13 13:36:10
tags: npm
---

1. 快速初始化package

    用```npm init```來初始化package, npm會問一連串的問題. 如果想要略過, 可以加上參數-y
    ```
    npm init -y
    ```
    我們可以用```npm config```預先設置初始化的設定, 這樣下次用快速初始化時就可以自動幫我們填上
    ```
    npm config set init-author-name 'Jim Chen'
    npm config set init-author-email 'jimchen@test.com'
    ```
2. 從其他來源來安裝package

    NPM CLI允許我們從其他來源安裝package
    ```
    # 從Bit安裝
    npm config set @bit:registry https://node.bit.dev
    npm i @bit/username.collection.component

    # 從Github安裝
    npm i githubuser/reponame

    # 從BitBucket安裝
    npm i bitbucket:bitbucketuser/reponame

    # 從gist安裝
    npm i gist:gistID
    ```
3. 使用```npm ci```可靠地安裝一個package
    
    NPM提供CI指令
    ```bash
    npm ci
    ```
    它是以```package-lock.json```來得知安裝依賴的package, 並使用```package.json```來驗證是否有不匹配的版本, 如果不一致, 則將引發錯誤, 它會跳過一些使用者相關的功能, 因此速度較快, 適合用在CI或自動化作業中.
   * 專案項目中必須有一個```package-lock.json```
   * 如果```package-lock.json```中的依賴項不匹配, 則引發錯誤
   * 刪除```node_modules```並重新安裝
   * 不會寫入```package.json```或```package-lock.json```

4. 使用縮寫來安裝package

    ```bash
    # Install package
    npm install <package_name>
    npm i <package_name> # 

    # Install devDependencies
    npm install --save-dev <package_name>
    npm i -D <package_name>

    # Install dependencies (default)
    npm install --save-prod <package_name>
    npm i -P <package_name>

    # Install packages globally
    npm install --global <package_name>
    npm i -g <package_name>
    ```
    
    當有多個package要一起安裝時, 用空白符號分隔
    ```bash
    npm i express axios
    ```

    當有多個package要一起安裝, 且它們有相同的prefix時, 可以用{}和逗號來區分
    ```bash
    npm i eslint-{plugin-import, plugin-react, loader}

    # 等同如下
    npm i eslint-plugin-import eslint-plugin-react eslint-loader
    ```
5. 快速打開某個package的文件
   
    ```bash
    npm docs <package-name>
    # 或
    npm home <package-name>
    ```
   如果想要看看某個package是不是有任何issue或bug, 可以用下列指令快速開啟
   ```bash
   npm bug <package_name>
   ```
   如果想看看package的GitHub repository, 可以用下列指令快速開啟
   ```bash
   npm repo <package_name>
   ```
6. 移除重覆的package
   
    我們可以用下列指令來移除重覆的依賴項
    ```bash
    npm dedupe
    # 或
    npm ddp
    ```
7. 檢查與修復專案中的package漏洞

   ```bash
   # 檢查漏洞
   npm audit

   # 檢查並自動修復漏洞(如果修復版本已存在)
   npm audit fix
   ```

8. 檢查過時的package

    我們可以使用下列指令來列出專案中已有更新版本的package
    ```bash
    npm outdated --long
    # 或
    npm outdated -l
    ```
    另外, 我們也可以用下列指令來檢查某個package的版本資訊
    ```bash
    npm view package <package_name>
    # 或
    npm v <package_name>
    
    # 只顯示最新版號
    npm v <package_name> version

    # 顯示所有版號
    npm v <package_name> versions
    ```
    