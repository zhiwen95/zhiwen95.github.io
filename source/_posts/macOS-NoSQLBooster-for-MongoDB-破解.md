---
title: NoSQLBooster for MongoDB 破解
date: 2020-10-09 17:13:23
tags: 
  - 破解
  - 软件
---

NoSQLBooster for MongoDB 基于 Electro 编写 asar 打包，所以我们能够解包修改代码并重新打包。
<!-- more -->
1. 安装工具

   ```bash
   npm install asar -g
   ```

2. 解包，进入 /Applications/NoSQLBooster for MongoDB.app/Contents/Resources (Windows 的话搜一下 app.asar 文件)

   ```bash
   asar extract app.asar app
   ```

3. 修改 app\shared\lmCore.js 里的 MAX_TRIAL_DAYS 和 TRIAL_DAYS 值

   ```javascript
   MAX_TRIAL_DAYS=3000,TRIAL_DAYS=3000
   ```

4. 打包，打包完之后删除 app 文件夹

   ```bash
   asar pack app app.asar
   ```

5. 重启软件，效果如下

   ![image-20201009173410454](result_show.png)
