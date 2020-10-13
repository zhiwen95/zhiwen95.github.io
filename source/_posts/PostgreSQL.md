---
title: PostgreSQL
date: 2020-10-13 11:44:57
tags:
---

## 配置

### 时区设置

设置 database 的时区

```sql
ALTER DATABASE postgres SET timezone TO 'Asia/Shanghai';
```

临时修改当前连接的时区

```sql
SET TIME ZONE "Asia/Shanghai";
```

默认时区需要修改配置文件 postgresql.conf 修改后需重启 PostgreSQL 服务

```properties
timezone = 'Asia/Shanghai'
log_timezone = 'Asia/Shanghai'
```
