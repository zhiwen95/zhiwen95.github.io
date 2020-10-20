---
title: SecureCRT
date: 2020-10-19 19:03:45
tags: 
  - 软件
  - SecureCRT
  - 破解
---

## 免费试用/无限试用

通过脚本定期清除 lic 文件即可无限试用，我列举的是 macOS 的方法

<!-- more -->

1. SecureCRT 的配置目录文件如下

  ```shell
  $ ll /Users/weizhiwen/Library/Application\ Support/VanDyke/SecureCRT/Config/
  total 368
  -rw-r--r--   1 weizhiwen  staff    24B 11 12  2018 ButtonBarV4.ini
  -rw-r--r--   1 weizhiwen  staff    24B  9 14 13:12 ButtonBarV5.ini
  -rw-r--r--   1 weizhiwen  staff    79K  9 25 11:34 FileTypes.ini
  -rw-r--r--   1 weizhiwen  staff    22K 10 20 10:21 Global.ini
  drwx------  38 weizhiwen  staff   1.2K 10 20 10:21 KnownHosts
  -rw-r--r--   1 weizhiwen  staff   432B 10 19 17:16 Recent File List SecureCRT.ini
  -rw-r--r--   1 weizhiwen  staff   198B 10 20 10:21 Recent File List SecureFX.ini
  -rw-r--r--   1 weizhiwen  staff   874B 10 20 10:21 SSH2.ini
  -rw-r--r--   1 weizhiwen  staff   239B 10 12 17:08 SecureCRT_eval.lic
  -rw-r--r--   1 weizhiwen  staff   239B 10 20 10:21 SecureFX_eval.lic
  drwxr-xr-x   6 weizhiwen  staff   192B  9 21 13:28 Sessions
  ```

2. 创建删除 lic 的脚本，我用的文件名是 ~/.script/zhiwen.file.clean.sh 

  ```shell
  #!/bin/bash
  rm -rf /Users/weizhiwen/Library/Application\ Support/VanDyke/SecureCRT/Config/*.lic
  ```

3. 创建定时任务配置，我用的文件名是 ~/Library/LaunchAgents/zhiwen.file.clean.plist，这里使用的是 macOS 的 launchctl 命令，需要修改 Label/ProgramArguments/StandardOutPath/StandardErrorPath 四个参数

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
       <dict>
           <key>Label</key>
           <string>zhiwen.file.clean</string>
           <key>RunAtLoad</key>
           <true/>
           <key>ProgramArguments</key>
           <array>
               <string>bash /Users/weizhiwen/.script/zhiwen.file.clean.sh</string>
           </array>
           <key>StartInterval</key>
           <integer>1209600</integer>
           <key>StandardOutPath</key>
           <string>/Users/weizhiwen/.script/logs/zhiwen.file.clean.log</string>
           <key>StandardErrorPath</key>
           <string>/Users/weizhiwen/.script/logs/zhiwen.file.clean.error.log</string>
       </dict>
   </plist>
   ```

4. 加载定时任务配置

   ```shell
   $ cd ~/Library/LaunchAgents
   # 加载定时任务
   $ launchctl load -w zhiwen.file.clean.plist
   # 修改配置后要先 unload 再 load
   $ launchctl unload zhiwen.file.clean.plist
   # 立即执行
   $ launchctl start zhiwen.file.clean.plist
   ```

   

## 设置

> 为了防止世界被破坏 为了维护世界的和平 我需要设置一下 SecureCRT 🤣

### 关闭标签的标题变更功能

设置后可以使打开的标签的标题显示成 session 的名称，方便辨识服务器

1. 点击菜单栏 Options
2. 点击 Edit Default Session...
3. Terminal > Emulation > Advanced
4. 选中 Ignore window title change requests
5. 点击 OK 选择 Change ALL Sessions