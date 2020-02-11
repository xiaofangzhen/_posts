---
title: SQL常用语句
date: 2020-02-11 16:40:12
tags: SQL
---

新建用户： 
```bash
CREATE USER 'username'@'host' IDENTIFIED BY 'passwd';
```

授权：
```bash
GRANT privileges ON dbname.table TO 'username'@'host';
```

建库：
```bash
create database dbname
```

刷新权限：
```bash
flush privileges;
```

